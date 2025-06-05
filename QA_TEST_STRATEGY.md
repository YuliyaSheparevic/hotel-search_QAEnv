**Introduction**

This document defines the testing strategy for validating the hotel_booking application. The QA approach consists of both manual testing and automated tests to ensure quality and robustness of the application.

**1. Manual QA Testing Strategy**

1.1 Key User Flows and Priority Test Cases

Key user flows focus on core functionality of the app. These scenarios are categorized based on priority:

| Feature | User Flow/Scenario | Expected Outcome | Priority |
| :-- | :-- | :-- | :-- |
| Login | User logs in with valid credentials. | User logs in successfully, and the dashboard is loaded. | High |
|  | User logs out. | User is redirected to the login screen. | High |
| Favorites | Save a hotel to the favorites list. | Hotel is added to the favorites list. | High |
|  | Remove a hotel from the favorites list. | Hotel is removed from the list. | High |
| Hotels Search | Search for hotels in a specific location. | Relevant hotels are displayed in the results. | High |
|  | Pagination when scrolling hotel results. | Next page of results is loaded (API state validations). | High |
|  | Handle empty search results. | "No results found" message is displayed in the UI. | Medium |
| Dashboard | View user statistics and analytics (if applicable). | Analytics and relevant data are displayed correctly for the logged-in user. | Medium |
| Localization | Change the app language (e.g., English → French). | UI text updates correctly to the selected language. | Medium |
| Errors/Edge Cases | Display error state for API failures on search or favorites loading. | User sees a "Something went wrong" message in case of errors. | High |

1.2 Description of State Transitions

State transitions validate the behavior of the app when users perform key actions such as logging in/out, interacting with search features, or modifying the favorites list. Below are the identified transitions:

| Module | Action | State Before | State After | Expected Outcome |
| :-- | :-- | :-- | :-- | :-- |
| Login | User logs in. | No authenticated session. | Authenticated session created. | User redirected to the my account page. |
|  | User logs out. | Authenticated session active. | Authenticated session removed. | Login screen displayed; all sensitive user data cleared. |
| Hotels Search | User submits a search. | Idle search state. | Loading state, then results. | Results are fetched and displayed on the UI. |
|  | User scrolls for pagination. | Initial page loaded. | Next page loaded. | New results appended to the list without data duplication. |
|  | API error occurs. | Hotel search in progress. | Error state visible. | Proper "error message" with retry option shown. |
| Favorites | User adds a favorite. | Hotel not saved in favorites. | Hotel added to favorites. | Favorites list updates in both UI and persistent storage (Hive). |
|  | User removes a favorite. | Hotel exists in favorites list. | Hotel removed from list. | UI updates instantly and backend sync is validated. |


1.3 UI Validation for Main Screens

a. Favorites Page

Empty state: The page should display a message such as "You have no favorites" when the list is empty.

Add favorite: Verify that hotels appear correctly with their images, names, and details.

Remove favorite: Ensure the hotel is removed both visually and from the backend database.

b. Hotels Search Page

Search bar functionality:

The user can type a search query and see suggestions while typing.

Search button triggers the results display.

Search results:

Cards should display hotel name, location, and price.

Pagination works as expected, appending data smoothly.

Error state:

Proper messaging shown if no results are found or the API call fails.

c. Login Page

Form validation:

Display proper validation errors for empty or incorrect input (e.g., missing '@' in email, incorrect password, empty login or so on).

Successful login: Redirect to the my account page.

Invalid login: Display a failure message such as "Invalid email or password."

d. Localization

Validate that hotel names, labels, and buttons are updated per the selected language.

Check if right-to-left (RTL) behavior is handled correctly for RTL-supported languages like Arabic.

1.4 Test Data Preparation

Test data preparation ensures scenarios are properly set up for manual and automated validations.

Accounts for Login Module
| Account Type | Email | Password | Expected Role |
| :-- | :-- | :-- | :-- |
| Admin User | admin@hotelbooking.com | password123 | Access to all features. |
| Regular User | user@hotelbooking.com | password123 | Access only as a customer. |
| Invalid User | invalid@noemail.com | wrongpassword | Displays "Invalid credentials." |



