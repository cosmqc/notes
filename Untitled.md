|            |              |                                                                                                                                             |
| ---------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Story / AC | Estimate (h) | Justification                                                                                                                               |
| U1         | 2h           | Verify the change to cucumber tests hasn’t broken anything.                                                                                 |
| U4 AC6     | 2h           | Change edit profile frontend validation to include name length rules. Verify other name input fields perform validation correctly.          |
| U8         | 1h           | Change description text to 'Describe your garden' instead of 'Describe your plant'. Disallow a garden size of zero on frontend and backend. |
| U10 AC4    | 2h           | Add input validation for location inputs.                                                                                                   |
| U11 AC3    | 2.5h         | Add error handling for long plant names. Possibly restrict length to a reasonable number.                                                   |
| U11 AC6    | 2.5h         | Add error handling for planted dates in the future.                                                                                         |
| U12 AC3    | 1h           | Verify the change to the edit plant button passes all ACs and NFRs.                                                                         |
| U12 AC4    | 2h           | Add error handling for long plant names. Possibly restrict length to a reasonable number.                                                   |
| U12 AC8    | 2h           | Add error handling for planted dates in the future and unreasonably long ago.                                                               |
| U13        | 0.5h         | Verify the change to the image '+' button passes all ACs and NFRs.                                                                          |
| U13 AC5    | 0.5h         | Change size limit from 10MiB to 10MB.                                                                                                       |
| U13        | 2h           | Add authorization logic for the 'upload image' endpoint.                                                                                    |
| U14        | 1h           | Link weather logic to the garden's location.                                                                                                |
| U14        | 7h           | Reduce tech-debt for weather backend.                                                                                                       |
| U14 AC6    | 7h           | Correct alert-disabling logic that allows the alert to be closed until the next day.                                                        |
| U15 AC6    | 8h           | Add location autocomplete functionality.                                                                                                    |
| U15        | 8h           | Reduce tech-debt for location backend.                                                                                                      |
| U15        | 4h           | Improve UX for location features.                                                                                                           |
| U17        | 5h           | Improve UX for friend features.                                                                                                             |
| U17 AC4    | 4h           | Combine first name / last name fields into one search bar.                                                                                  |
| U17        | 1h           | Fix path issues with friends features on deployment.                                                                                        |
| U18 AC1    | 2h           | Fix issue where user A can accept a canceled friend request from user B if user A hasn't refreshed the page yet.                            |
| U19        | 3h           | Fix issue where editing a garden description resets the publicity setting.                                                                  |
| U20        | 0.5h         | Remove image upload button from a public garden's page.                                                                                     |
|            |              |                                                                                                                                             |
