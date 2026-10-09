# ICE Task 3 – Album Collection & Debugging

## 1. Introduction

The Album Collection application is a React Native mobile application developed with Expo and TypeScript. It allows a user to enter an album's title, artist, release year, genre, and rating. The user can add valid albums to a favourites collection, view the saved albums in a list, and delete an album when it is no longer needed.

The purpose of this ICE task was to inspect an existing application, identify errors, correct the code, and test the application. The original application structure and purpose were retained while correcting its validation, state management, picker values, and deletion behaviour.

## 2. Development Environment

The application is intended to be developed and tested using:

- **React Native** – provides the mobile user interface.
- **Expo** – runs and supports development of the React Native application.
- **TypeScript** – provides types for the album object and application state.
- **Institutional VM** – the required development environment for this task.
- **BlueStacks 5** – the Android emulator used to test the application.
- **Expo Go** – opens the development version of the application in the emulator.
- **Visual Studio Code** – used to edit `App.tsx` and the README.

The assignment requires the completed application to be tested in BlueStacks 5 using Expo Go. Testing through a web browser can be useful for initial debugging, but it does not replace the required emulator test.

## 3. Error Log

The following table records the problems identified in the supplied code and the corrections made in the corrected version. Keep only the entries that match the changes you actually made and verified.

| # | Location | Problem | Error type | Correction |
|---:|---|---|---|---|
| 1 | `Album` type | The `year` and `rating` fields were typed as strings, but the saved object used numeric values. | TypeScript | Changed `year` and `rating` to `number` so the type matches the values stored in an album. |
| 2 | `validateForm()` – title | The title length condition used `&&`. A value cannot normally be shorter than the minimum and longer than the maximum at the same time, so the check did not work as intended. | Logic | Changed the condition to `||` so titles outside the allowed range are rejected. |
| 3 | `validateForm()` – artist | The artist length check also used `&&`, preventing the intended length validation. | Logic | Changed the condition to `||`. |
| 4 | `validateForm()` – year | The original validation checked that the year was not below 1900 but did not reject a year in the future. | Validation | Added a check that the year is between 1900 and the current year. |
| 5 | `validateForm()` – rating | The original code rejected ratings below 1 but did not reject ratings above 5. | Validation | Added an upper-bound check so ratings must be whole numbers from 1 to 5. |
| 6 | `handleSave()` | `setAlbums([temporaryAlbum])` replaced the existing collection each time a new album was saved. | State management / logic | Changed the update to `setAlbums((currentAlbums) => [...currentAlbums, temporaryAlbum])` to append the new album. |
| 7 | Genre `Picker` | `selectedValue` was connected to `title` rather than `genre`. | Input / state | Connected `selectedValue` to `genre`. |
| 8 | Genre `Picker.Item` | Every genre option used the current `genre` as its value, rather than the mapped genre option. | Input / logic | Used `value={item}` so each option returns its own genre. |
| 9 | `handleDelete()` | The filter condition used `album.id === id`, which retained only the selected album instead of removing it. | Logic | Changed the condition to `album.id !== id` so the selected album is removed and the others remain. |
| 10 | `FlatList` | The album title was used as the list key, although titles may not be unique. | List / rendering | Changed `keyExtractor` to use each album's unique `id`. |

## 4. Testing

Test the application after applying the corrections. Record the actual result of each test before submitting this README.

| Test | Procedure | Expected result | Actual result |
|---|---|---|---|
| Initial launch | Open the application in the required emulator. | The interface opens without unexpected errors. | Pending testing |
| Empty form | Press **Add to Favourites** without entering information. | A validation alert appears and no album is added. | Pending testing |
| Invalid title or artist | Enter a title or artist with fewer than 2 characters, or more than 50 characters. | A validation alert appears and the album is not added. | Pending testing |
| Invalid year | Enter a year below 1900, a future year, or a non-whole number. | A validation alert appears and the album is not added. | Pending testing |
| Invalid rating | Enter 0, a number above 5, or a decimal. | A validation alert appears and the album is not added. | Pending testing |
| Valid album | Enter valid information in every field and submit. | The album appears with the correct title, artist, year, genre, and rating. | Pending testing |
| Multiple albums | Add at least three different albums. | All added albums remain in the collection. | Pending testing |
| Delete album | Delete one album when multiple albums are displayed. | Only the selected album is removed. | Pending testing |
| Continue using app | Add an album after deleting another. | The collection continues to update correctly. | Pending testing |

**Testing note:** Replace “Pending testing” with what actually happened after you test each scenario. Do not report a test as successful unless you have performed it.

## 5. Screenshot

Insert a screenshot of the completed application running in **BlueStacks 5 using Expo Go**, as required by the task.

For example, save the screenshot in the project as `screenshots/album-collection.png` and add it to this section using:

```markdown
![Album Collection application running in BlueStacks 5 using Expo Go](screenshots/album-collection.png)
```

Create the `screenshots` folder and add your own screenshot file before submitting. The image must be present in the repository for the Markdown image to display.

## 6. Conclusion

This task provided practice in reading and debugging an existing React Native and TypeScript application. The corrections addressed validation conditions, the types used for album data, state updates, genre selection, list keys, and deletion logic. Testing the application with valid and invalid input helps confirm that albums are handled correctly and that the collection remains usable after items are added or removed.

