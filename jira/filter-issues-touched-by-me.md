Filter Issues Touched By Me
===========================

Finding stuff in JIRA can be a pain. Creating two filters to grab all issues that I touched is super useful: one for closed issues and one for issues that are still open.

## Done and touched by me

```
(summary ~ currentUser() OR description ~ currentUser() OR assignee = currentUser() OR assignee was currentUser() OR worklogAuthor = currentUser() OR comment ~ currentUser() OR watcher = currentUser() OR text ~ currentUser() OR creator = currentUser() OR voter = currentUser() OR Status changed by currentuser()) AND status = Closed ORDER BY lastViewed DESC
```

## TODO and touched by me

```
(summary ~ currentUser() OR description ~ currentUser() OR assignee = currentUser() OR assignee was currentUser() OR worklogAuthor = currentUser() OR comment ~ currentUser() OR watcher = currentUser() OR text ~ currentUser() OR creator = currentUser() OR voter = currentUser() OR Status changed by currentuser()) AND status not in (Done, Closed) ORDER BY lastViewed DESC
```

[Sourced from Atlassian forums](https://community.atlassian.com/t5/Jira-questions/How-can-I-filter-for-all-issues-where-I-have-commented/qaq-p/223917#M266288)
