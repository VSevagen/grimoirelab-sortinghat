# Filter through profiles

Looking for a particular profile ? SortingHat provides several filters which can be used to filter through the lists of individuals to find the required one. You can filter the profiles according to the following filters.<br>

- <code style="background-color: #FBE5E1; color: #C0341D; padding: 0 0.4rem; font-size:15px;">isBot</code> <br> Filter profiles marked as bots. For example `isBot: true` will return all profiles marked as bot and vice versa.<br>
  ![is-bot](./assets/is-bot.png)<br>
- <code style="background-color: #FBE5E1; color: #C0341D; padding: 0 0.4rem; font-size:15px;">isLocked</code> <br> Filter profiles marked as locked. For example `isLocked: true` will return all profiles marked as locked and vice versa<br>
- <code style="background-color: #FBE5E1; color: #C0341D; padding: 0 0.4rem; font-size:15px;">country</code> <br> Filter using either country name or country code . For example `country: "United States of America` and `country: USA` return the same result.<br>
- <code style="background-color: #FBE5E1; color: #C0341D; padding: 0 0.4rem; font-size:15px;">gender</code> <br> Filter profiles based on their gender. For example `gender: non binary`<br>
- <code style="background-color: #FBE5E1; color: #C0341D; padding: 0 0.4rem; font-size:15px;">source</code> <br> Filter based on data source. For example `source: Github`<br>
- <code style="background-color: #FBE5E1; color: #C0341D; padding: 0 0.4rem; font-size:15px;">enrollement</code> <br> Filter based on organisations. For example `enrollment: "Bitergia"`<br>
- <code style="background-color: #FBE5E1; color: #C0341D; padding: 0 0.4rem; font-size:15px;">isEnrolled</code> <br> Filter based on enrollement status. For example `isEnrolled: true` will return all profiles currently enrolled at some organisation and vice versa<br>
- <code style="background-color: #FBE5E1; color: #C0341D; padding: 0 0.4rem; font-size:15px;">enrollmentDate</code> <br>
  Filter profiles based on when they were affiliated to an organisation. <br>

  | Filter                                             | Explanation                                                                              |
  | -------------------------------------------------- | ---------------------------------------------------------------------------------------- |
  | <code>enrollmentDate:>YYYY-MM-DD</code>            | Matches individuals that were affiliated to an organization after the given date.        |
  | <code>enrollmentDate:>=YYYY-MM-DD</code>           | Matches individuals that were affiliated to an organization on or after the given date.  |
  | <code>enrollmentDate:&lt;YYYY-MM-DD</code>         | Matches individuals that were affiliated to an organization before the given ;date.      |
  | <code>enrollmentDate:<=YYYY-MM-DD</code>           | Matches individuals that were affiliated to an organization on or before the given date. |
  | <code>enrollmentDate:YYYY-MM-DD..YYYY-MM-DD</code> | Matches individuals that were affiliated to an organization between the given dates      |

- <code style="background-color: #FBE5E1; color: #C0341D; padding: 0 0.4rem; font-size:15px;">lastUpdated</code> <br>
  Filter profiles based on when they were modified. <br>

  | Filter                                          | Explanation                                                       |
  | ----------------------------------------------- | ----------------------------------------------------------------- |
  | <code>lastUpdated:>YYYY-MM-DD</code>            | Matches individuals that were updated after the given date        |
  | <code>lastUpdated:>=YYYY-MM-DD</code>           | Matches individuals that were updated on or after the given date. |
  | <code>lastUpdated:&lt;YYYY-MM-DD</code>         | Matches individuals that were updated before the given date.      |
  | <code>lastUpdated:<=YYYY-MM-DD</code>           | Matches individuals that were updated on or before the given date |
  | <code>lastUpdated:YYYY-MM-DD..YYYY-MM-DD</code> | Matches individuals that were updated between the given dates.    |

  <br>
