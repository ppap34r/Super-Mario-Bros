# Super Mario Bros.

Classic Super Mario Bros. game implemented with Java for CS319-Object-Oriented Software Engineering course.

## About game

You can visit [wikipedia page](https://en.wikipedia.org/wiki/Super_Mario_Bros.) or [Super Mario wiki page](https://www.mariowiki.com/Super_Mario_Bros.) for detailed information about the game.

## Built With
* [Java](https://www.java.com/)
* [Maven](https://maven.apache.org/) or [Gradle](https://gradle.org/)
* [JUnit 5](https://junit.org/junit5/)

## Build and Test

The project uses the standard Maven/Gradle source layout. Production code is in
`src/main/java`, game resources are in `src/main/resources/media`, and new unit
tests belong in `src/test/java`.

Run the complete test suite with either supported build tool:

```bash
mvn test
```

```bash
./gradlew test
```

Maven is the primary command for the course demonstration because it is available
in this workspace. Gradle uses the same JUnit 5 test suite and is provided as an
equivalent build configuration through the included Gradle Wrapper.

## JUnit 5 Test Boilerplate

Create a separate test class under `src/test/java` with the package that matches
the production class being tested. Replace the copyright holder before committing
the file. This project uses JUnit 5, so the setup and cleanup annotations are
`@BeforeEach` and `@AfterEach` rather than JUnit 4's `@Before` and `@After`.

```java
/* Copyright (C) 2026 <Full Team Member Names> - All Rights Reserved
 * You may use, distribute and modify this code under the terms of the MIT license.
 */
package model;

import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertThrows;

class GameObjectTest {

    private GameObject gameObject;

    @BeforeEach
    void setUp() {
        gameObject = new GameObject(10, 20, null) { };
    }

    @AfterEach
    void tearDown() {
        gameObject = null;
    }

    @Test
    void setX_updatesHorizontalPosition() {
        gameObject.setX(42);

        assertEquals(42, gameObject.getX());
    }

    // Example exceptional-behaviour assertion:
    // assertThrows(IllegalArgumentException.class,
    //         () -> methodUnderTest(invalidInput));
}
```

The code above is a template, not one of the required 10 assignment test cases.
Use the designed ISP values and expected outcomes in place of the examples. Do
not keep the exception example unless the selected production method actually
throws `IllegalArgumentException`.

## In-game Screens

### Start Screen
![start screen](https://raw.githubusercontent.com/ahmetcandiroglu/1G.Super-Mario-Bros/master/docs/Screenshots/Start%20screen.png)

### Inside Game
![in game screen](https://raw.githubusercontent.com/ahmetcandiroglu/1G.Super-Mario-Bros/master/docs/Screenshots/In%20game%20screen.png)

### Pause Screen
![pause screen](https://raw.githubusercontent.com/ahmetcandiroglu/1G.Super-Mario-Bros/master/docs/Screenshots/Pause%20screen.png)
