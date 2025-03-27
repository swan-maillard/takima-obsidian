  
## 🎓 Context
During this milestone, we were asked the following objectives:
- Get familiar with **JUnit** and **AssertJ**
- Add **Unit tests** on our services using **mock data** with **mockito**
- Add **Integration tests** on our services and controllers using **Test Containers**

## 📝 Progress
I have produced the following bonuses:
- Created fake **migration scripts** for testing
- Created an annotation to **reset the database** after tests => avoids using **transactional**

## 🤔 Difficulties
It went quite well, but it is hard to know which methods should be tested through unit tests, or integration tests.
It is also hard to know if the integration should be done on the controllers, or the services, or both; but that would mean repeating the "same" tests since controllers are simple gateways to the services.

