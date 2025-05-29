---
sidebar : 3
---

# BLoC Layer 🧱

| **Component**        | **Description** |
|----------------------|-----------------|
| **State file 💽**     | Holds the reference to the data you want to display in the UI |
| **Event file ▶︎**     | Holds the reference to events triggered from the UI |
| **BLoC file 🔗**      | Connects State and Event, performs logic, and emits newState |

### 1. Creating the Events file ⏭︎

In BLoC, if a user wants to send the data from the UI to BLoC or they want to add any kind of triggers then it is done via events. Here're some things that you can keep in mind while creating the events.

- Create a sealed class instead of an abstract class for the events. [Reference](https://dart.dev/language/class-modifiers)
- Whenever implementing these sealed classes, create a final class for it.

:::tip
Events should be named in the past tense because events are things that have already occurred from the bloc's perspective.
:::

Here's an example for it:

```jsx title="lib/modules/repository/home_repository.dart"
part of 'home.bloc.dart';

sealed class HomeEvent extends Equatable {
  const HomeEvent();

  @override
  List<Object> get props => [];
}

final class HomeGetPostEvent extends HomeEvent {
  const HomeGetPostEvent();
}
```

:::tip
- Initial load events should follow the convention: **BlocSubject + Started**
- The base event class should be name: **BlocSubject + Event**
:::

### 2. Creating the State file 📌

Anyone watching this documentation would know about the `State class` because `BLoC State Management `is the basic requirement of this boilerplate.

Thus, the requirement of writing about the `State Class` is to specify the format we're gonna use to create `State Classes` in the project.

Let's continue the example of the Home feature 😉:

```jsx title="lib/modules/home/bloc/home_state.dart"
part of 'home.bloc.dart';

class HomeState extends Equatable {
  final List<HomeModel> postsList;
  final bool hasReachedMax;
  final ApiStatus status;
  const HomeState._({
    this.postsList = const <HomeModel>[],
    this.hasReachedMax = false,
    this.status = ApiStatus.initial,
  });

  const HomeState.initial() : this._(status: ApiStatus.initial);
  const HomeState.loading() : this._(status: ApiStatus.loading);
  const HomeState.loaded(List<HomeModel> postList, bool hasReachedMax)
      : this._(
          status: ApiStatus.loaded,
          postsList: postList,
          hasReachedMax: hasReachedMax,
        );
  const HomeState.error() : this._(status: ApiStatus.error);

  HomeState copyWith({
    ApiStatus? status,
    List<HomeModel>? postsList,
    bool? hasReachedMax,
  }) {
    return HomeState._(
      status: status ?? this.status,
      postsList: postsList ?? this.postsList,
      hasReachedMax: hasReachedMax ?? this.hasReachedMax,
    );
  }

  @override
  List<Object?> get props => [postsList, hasReachedMax, status];

  @override
  bool get stringify => true;
}
```

- In this approach, we tried to merge 2 approaches together so that anyone can work with either of them without facing any issues in it. This class contains both `Named Constructor` and `Copy with` methods that developers can use to emit states.

- This example of state is for the paginated data. `ApiStatus` is an enum that can be found in the `lib/app/enum.dart` file.

:::tip
The base state class should always be named: BlocSubject + State
:::

### 3. Creating the BLoC file 🟦

`BLoC` file is one of the core files of this whole API integration process. Because `BLoC` emits states in response to an incoming event within an `EventHandler`.

Let's continue the example of the Home feature for implementing the BLoC:

```jsx title="lib/modules/home/bloc/home_bloc.dart"
class HomeBloc extends Bloc<HomeEvent, HomeState> {
  HomeBloc({required this.repository}) : super(const HomeState.initial()) {
    /// Here, we're using droppable transformer, because it will process
    /// only one event and ignore (drop) any new events until the current event is done.
    on<HomeGetPostEvent>(_onHomeGetPostEvent, transformer: droppable());
  }
  final IHomeRepository repository;

  int _pageCount = 1;

  FutureOr<void> _onHomeGetPostEvent(
    HomeGetPostEvent event,
    Emitter<HomeState> emit,
  ) async {
    if (state.hasReachedMax) return;

    /// If the user is coming for the first time then show the loader, it that's not the case
    /// that means user wants to more load data, which implies that they should have some data
    /// That's why we're not emitting the loading state in case the user has any data.
    state.status == ApiStatus.initial
        ? emit(const HomeState.loading())
        : emit(HomeState.loaded(state.postsList, false));
    final fetchPostEither = await repository.fetchPosts(page: _pageCount).run();
    fetchPostEither.fold(
      (error) => emit(const HomeState.error()),
      (result) {
        emit(
          HomeState.loaded(
            state.postsList.followedBy(result).toList(),
            false,
          ),
        );
        _pageCount++;
      },
    );
  }
}
```
In this file, we're doing the following things:

- Taking an instance of the `Repository`.
- Adding an `_onHomeGetPostEvent` which will trigger the API call
- On `_onHomeGetPostEvent`, we're checking if we're adding this event for the first time or not, and based on it we're further triggering the API call.
- After the API call has been made and we've given the response, we're using the `fold` method of `fpdart` package, that gives us the error in case of any `Failure` and `result` in case of an successful API call.

### 4. Providing the BLoCs and Repositories in the UI 🎁

You've already created the UI in the first step. But injecting the `BLoC` and `Repository` will also happen in this file, because we want to scope our `BLoCs` and `Cubits` to its respective modules.

Let's look at the example for it:

```jsx title="lib/modules/home/screen/home_screen.dart"
class HomeScreen extends StatefulWidget implements AutoRouteWrapper {
 const HomeScreen({super.key});

 @override
 Widget wrappedRoute(BuildContext context) {
   return RepositoryProvider<HomeRepository>(
     create: (context) => HomeRepository(),
     child: BlocProvider(
       lazy: false,
       create: (context) => HomeBloc(
         repository: RepositoryProvider.of<HomeRepository>(context),
       )..add(const HomeGetPostEvent()),
       child: this,
     ),
   );
 }

 @override
 State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
 @override
 Widget build(BuildContext context) {
   return Scaffold(...)
   }
}
```

- Here, we're using `AutoRouteWrapper` which is provided by AutoRoute package.
- By implementing `AutoRouteWrapper`, we've to override one method called wrappedRoute. In this method, we've to provide the `BlocProvider` and/or `RepositoryProvider` in this function.
- After we add this, we've to generate the necessary files by using the build runner. You can run this command in the terminal to run the build runner.

```
flutter packages pub run build_runner build
```