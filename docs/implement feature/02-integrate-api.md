---
sidebar : 2
---

# Integrating API in Repository 🌐

API integration is the core part of any App. Because it involves error handling, data fetching, data manipulating and so on. We'll use [fp_dart](https://pub.dev/packages/fpdart) to handle all the logic throughout the App.

To integrate any API in your Flutter app, follow the steps below.

 - Any API integration process starts from the repository file. Because in this file, user will write the actual logic of error handling and data manipulating (converting JSON to Dart objects)
- Let's take an example of a GET request. To implement it, create an abstract interface class like shown below:

```
abstract interface class IHomeRepository {
 /// This function returns TaskEither. In this, Task is indicating that this function
 /// is returning Future and Either is indicating that the function can either
 /// successfully return a value or return a Failure Object.
 TaskEither<Failure, List<HomeModel>> fetchPosts();
}
```
- Here, we're declaring a method called `fetchPosts` that returns a [TaskEither](https://www.sandromaglione.com/articles/how-to-use-task-either-fpdart-functional-programming). Meaning it can either return an Object of class `Failure` or it can successfully retrieve the data and send you the `List<HomeModel>`.


:::warning
This IHomeRepository is marked as abstract and interface, meaning we should override all the methods of the base class. So that no instance can be created of the IHomeRepository class. [Reference](https://dart.dev/language/class-modifiers)
:::

Now, let's divide the steps that you've to perform in the API integration 🔗, so that you can understand the whole flow of this:

1. Make an HTTP request 🎁
2. Check for a valid response ✔︎
3. Decode the response from JSON 🔁
4. Validate the response format and convert to Dart objects ✅

Finally, let's implement the IHomeRepository class step by step. We'll implement the class in the same file as it will be easier to find the implementation and abstract class in the same file.

### 1. Make an HTTP request 🎁

We'll create separate functions for each step described earlier. First, create a function that makes an API call and returns `TaskEither<Failure, Response>`.

```jsx title="lib/modules/repository/home_repository.dart"
class HomeRepository implements IHomeRepository {
 @override
 TaskEither<Failure, List<HomeModel>> fetchPosts() => makeFetchPostsRequest('posts');

 /// This functions calls the API and returns [Failure] in case of any error
 /// and [Response] in case of a successful API call
 TaskEither<Failure, Response> makeFetchPostsRequest(String url) {
   return ApiClient.request(
     path: url,
     queryParameters: {'_limit': 10},
     requestType: RequestType.get,
   );
 }
}
```

:::note
- Failure class will be integrated into the boilerplate.
- You can look up the implementation of it by going into `packages/api_client/lib/src/api-failure`.dart.
:::

### 2. Check for a valid response ✔︎

- The beauty of using `TaskEither` along with the function approach is that anyone can create their functions and chain them directly to the existing chain without knowing much about other functions.
- We can refactor the above code to chain multiple functions like this:

```jsx title="lib/modules/repository/home_repository.dart"
class HomeRepository implements IHomeRepository {
  @override
  TaskEither<Failure, List<HomeModel>> fetchPosts() => mappingRequest('posts');

  /// This mapping request function is basically a wrapper around all of the function
  ///  that makes API requets and hanldes the validation logic and Faliure handling
  TaskEither<Failure, List<HomeModel>> mappingRequest(String url) =>
      makefetchPostsRequest(url)
      .chainEither(checkStatusCode);

  TaskEither<Failure, Response> makefetchPostsRequest(String url, int page) {...}

  /// This functions checks if the status code is valid or not
  /// and based on that it returns the Response in case of success 
  /// or returns error in case of the Error.
  Either<Failure, Response> checkStatusCode(Response response) => 
      Either<Failure, Response>.fromPredicate(
        response,
        (response) => response.statusCode == 200 || response.statusCode == 304,
        (error) => APIFailure(error: error),
      );
}
```

### 3. Decode the response from JSON 🔁

- After you verify the status code, the next thing that we want to do is to convert the response of type `dynamic` to `Map<String,dynamic>`.
- But as we know that this can also give us an error, we'll create one other function that performs the operation of converting the `dynamic` response to `Map<String,dynamic>` response.
- Let's look at the implementation of this: 

```jsx title="lib/modules/repository/home_repository.dart"
class HomeRepository implements IHomeRepository {
  @override
  TaskEither<Failure, List<HomeModel>> fetchPosts() => mappingRequest('posts');

  TaskEither<Failure, List<HomeModel>> mappingRequest(String url) =>
      makeFetchPostsRequest(url)
      .chainEither(checkStatusCode)
      .chainEither(mapToList);
      

  TaskEither<Failure, Response> makeFetchPostsRequest(String url, int page) {...}

  Either<Failure, Response> checkStatusCode(Response response) {...};

  /// This function is responsible for converting the response to the dynamic list
  /// which can also return Failure in case of any casting Error. That's why it
  /// returns Either instead of List<dynamic>
  Either<Failure, List<Map<String, dynamic>>> mapToList(Response response) {
    return Either<Failure, List<Map<String, dynamic>>>.safeCast(
      response.data,
      (error) => ModelConversionFailure(error: error),
    );
  }
}
```

### 4. Validate the response format and convert to Dart objects ✅​

- The last step that we want to perform in this repository is to convert the` Map<String,dynamic> `into the Dart Models.
- As you might have guessed, we're gonna create a function for that too.

Let's look at the code for it:

```jsx title="lib/modules/repository/home_repository.dart"
class HomeRepository implements IHomeRepository {
  @override
  TaskEither<Failure, List<HomeModel>> fetchPosts() => mappingRequest('posts');

  TaskEither<Failure, List<HomeModel>> mappingRequest(String url, int page) =>
      makefetchPostsRequest(url, page)
          .chainEither(checkStatusCode)
          .chainEither(mapToList)
          .flatMap(mapToModel);

      

  TaskEither<Failure, Response> makefetchPostsRequest(String url, int page) {...}

  Either<Failure, Response> checkStatusCode(Response response) {...};

  Either<Failure, List<Map<String, dynamic>>> mapToList(Response response) {...}

  /// This function maps the List<Map<String,dynamic>> to List<HomeModel>. Since this conversion can also
  /// thow error, we have to return TaskEither.
  TaskEither<Failure, List<HomeModel>> mapToModel(List<Map<String, dynamic>> responseList) =>
      TaskEither<Failure, List<HomeModel>>.tryCatch(
        () async => responseList.map(HomeModel.fromJson).toList(),
        (error, stackTrace) => ModelConversionFailure(
          error: error,
          stackTrace: stackTrace,
        ),
      );
}
```

This concludes all the steps you've to perform in the `Repository Layer`.

Next thing you've to do is to implement this Repository in the `BLoC layer`.