---
sidebar : 2
---

# What is covered in this code generations?

### 1. Repository 📦

The Repository handles API interactions for fetching, saving, and deleting data.
- It wraps API calls in TaskEither for functional error handling and maps responses using RepositoryUtils.
- It also implements pagination by requesting data in pages.

### 2. Bloc Folder ⚡

The Bloc folder contains Bloc, which manages state changes and API calls. It defines three events:
- GetFeatureEvent: Fetches the initial data list.
- LoadMoreFeatureEvent: Loads more data for pagination.
- DeleteFeatureEvent: Removes an item from the list and updates the state.
The bloc maintains _page for tracking the pagination state and ensures efficient state updates.

### 3. Model 🏗️

The ResponseModel represents the API response, containing a list of Model items and pagination details.
- Model: Defines attributes like id, title, and description.
- oJson() and fromJson() handle serialization for API requests and responses.


### 4. Screen 🎨

The screen listens to Bloc using BlocBuilder and BlocListener. It displays data based on ApiStatus:
Loading: Shows a loader when fetching data.
- Loaded: Displays a list of Model items.
- Empty/Error: Shows appropriate messages when data is unavailable or API calls fail.


### 5. Pagination Functionality  🔄
Pagination is implemented using _page tracking and hasMorePages.
- The LoadMoreEvent requests the next page when needed.
- The droppable transformer ensures only one request runs at a time.
- New data is appended to the existing list while checking pagination.hasMorePages.