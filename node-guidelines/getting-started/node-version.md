## Node version

------
* [ ] **Use version 10 of node**
------

### Release schedule
![Node release chart](images/node-lts-schedule.png "Node release chart")

As of this document, the current LTS version of node is v10. A Current version receives minor and patch releases regularly and an Active version receives them monthly. As of October 2018, v10 will become an Active release so it is beneficial for us to already be on v10 so that we won't have to think about updating early next year when version 8 goes into Maintenance mode.

#### How the versioning works
New major releases occur every six months. Odd-numbered releases occur in October and are actively supported for 6 months. Even-numbered releases occur in April and are actively supported for 18 months (LTS).

It is beneficial to stay on LTS releases to ensure stability and to have a more predictable upgrade cycle.

> Odd numbered versions are non-LTS releases. They should only be used for evaluation and not in production.

**In production we should only use even-numbered LTS versions.**
