# [Spring development notes](https://spring.io/)

### Webflux

* Need a subscriber to a publisher before anything will actually happen.

### Testing

Spring has a concept of 'test slices'. Slices allow spring to only load the classes needed for the thing under test [^1]

[^1] https://developer.okta.com/blog/2018/09/24/reactive-apis-with-spring-webflux
