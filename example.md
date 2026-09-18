# Test 2 — `AuthorTestSEQA.java` (ACoC)

### **Function Under Test**

```java
public String getGivenFamily(boolean abbr)
```

---

### **2.1 Identify Testable Functions**

| Function                                                          
| -------------------| 
| `getGivenFamily()` |

---

### **2.2 Identify Parameters, Return Types, Return Values, and Exceptional Behavior**

**Parameters:** `abbr(boolean)`

**Return Type:** `String`

**Return Value:** The formatted author’s name (e.g., `"J. Smith"` or `"John Smith"`)

**Exceptional Behavior:** None

---

### **2.3 Model the Input Domain**

| Characteristic      | b1      | b2      |
| ------------------- | ------- | ------- |
| **C1 = abbr**       | True    | False   |
| **C2 = Given Name** | Present | Missing |
| **C3 = Suffix**     | Present | Missing |

---

### **2.4 Combine Partitions to Define Test Requirements**

**Assumption:** Choose all possible combinations.  
**Test Requirements (ACoC):** number of tests (upper bound) = 2 * 2 * 2 = **8 tests**

| TR  | (C1, C2, C3)              |
| --- | ------------------------- |
| TR1 | (True, Present, Missing)  |
| TR2 | (True, Present, Present)  |
| TR3 | (True, Missing, Missing)  |
| TR4 | (True, Missing, Present)  |
| TR5 | (False, Present, Missing) |
| TR6 | (False, Present, Present) |
| TR7 | (False, Missing, Missing) |
| TR8 | (False, Missing, Present) |

---

### **2.5 Derive Test Values**

| **Test ID** | **abbr** | **givenName, nameAbbr** | **familyName** | **suffix** | **Expected Result** |
| ----------- | -------- | ----------------------- | -------------- | ---------- | ------------------- |
| **T1**      | True     | `"John", "J."`          | `"Smith"`      | `null`     | `"J. Smith"`        |
| **T2**      | True     | `"John", "J."`          | `"Smith"`      | `"Jr."`    | `"J. Smith, Jr."`   |
| **T3**      | True     | `"", ""`                | `"Smith"`      | `null`     | `"Smith"`           |
| **T4**      | True     | `"", ""`                | `"Smith"`      | `"Jr."`    | `"Smith, Jr."`      |
| **T5**      | False    | `"John", "J."`          | `"Smith"`      | `null`     | `"John Smith"`      |
| **T6**      | False    | `"John", "J."`          | `"Smith"`      | `"Jr."`    | `"John Smith, Jr."` |
| **T7**      | False    | `"", ""`                | `"Smith"`      | `null`     | `"Smith"`           |
| **T8**      | False    | `"", ""`                | `"Smith"`      | `"Jr."`    | `"Smith, Jr."`      |

---


### **2.6. Test Case Descriptions**

| **Test ID** | **Test Case Name**                             | **Goal**                                                                                                                                                                                                                                 |
| ----------- | ---------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **T1**      | `getGivenFamily_AbbrFullNamePresentNoSuffix`   | The goal is to verify that when the abbreviation flag is set to true, and the author has a given name present but no suffix, the method returns the abbreviated given name followed by the family name in the format `"J. Smith"`.       |
| **T2**      | `getGivenFamily_AbbrFullNamePresentWithSuffix` | The goal is to verify that when the abbreviation flag is set to true, and the author has both a given name and a suffix present, the method returns the abbreviated given name, family name, and suffix in the format `"J. Smith, Jr."`. |
| **T3**      | `getGivenFamily_AbbrFullNameMissingNoSuffix`   | The goal is to verify that when the abbreviation flag is set to true, and the author has no given name and no suffix, the method returns only the family name in the format `"Smith"`.                                                   |
| **T4**      | `getGivenFamily_AbbrFullNameMissingWithSuffix` | The goal is to verify that when the abbreviation flag is set to true, and the author has no given name but has a suffix present, the method returns the family name and suffix in the format `"Smith, Jr."`.                             |
| **T5**      | `getGivenFamily_FullNamePresentNoSuffix`       | The goal is to verify that when the abbreviation flag is set to false, and the author has a given name present but no suffix, the method returns the full given name followed by the family name in the format `"John Smith"`.           |
| **T6**      | `getGivenFamily_FullNamePresentWithSuffix`     | The goal is to verify that when the abbreviation flag is set to false, and the author has both a given name and a suffix present, the method returns the full given name, family name, and suffix in the format `"John Smith, Jr."`.     |
| **T7**      | `getGivenFamily_FullNameMissingNoSuffix`       | The goal is to verify that when the abbreviation flag is set to false, and the author has no given name and no suffix, the method returns only the family name in the format `"Smith"`.                                                  |
| **T8**      | `getGivenFamily_FullNameMissingWithSuffix`     | The goal is to verify that when the abbreviation flag is set to false, and the author has no given name but has a suffix present, the method returns the family name and suffix in the format `"Smith, Jr."`.                            |


---

### **2.7. JUnit Test Implementation**

```java
/* Copyright (C) 2025 Chananphimon Chunchaowarit - All Rights Reserved
 * You may use, distribute and modify this code under the terms of the Chananphimon license.
 */

package org.jabref.model.entry;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

class AuthorTestSEQA {

    // Helper method to create a test Author object
    // Author(givenName, givenNameAbbreviated, namePrefix, familyName, nameSuffix)
    private Author createAuthor(String givenName, String givenNameAbbreviated, String familyName, String suffix) {
        return new Author(givenName, givenNameAbbreviated, null, familyName, suffix);
    }

    /**
     * Test Case 1: Abbr=True, GivenName=Present, Suffix=Missing. Expected: "J. Smith"
     */
    @Test
    void getGivenFamily_AbbrFullNamePresentNoSuffix() {
        Author author = createAuthor("John", "J.", "Smith", null);
        String result = author.getGivenFamily(true);
        assertEquals("J. Smith", result);
    }

    /**
     * Test Case 2: Abbr=True, GivenName=Present, Suffix=Present. Expected: "J. Smith, Jr."
     */
    @Test
    void getGivenFamily_AbbrFullNamePresentWithSuffix() {
        Author author = createAuthor("John", "J.", "Smith", "Jr.");
        String result = author.getGivenFamily(true);
        assertEquals("J. Smith, Jr.", result);
    }

    /**
     * Test Case 3: Abbr=True, GivenName=Missing, Suffix=Missing. Expected: "Smith"
     */
    @Test
    void getGivenFamily_AbbrFullNameMissingNoSuffix() {
        Author author = createAuthor("", "", "Smith", null);
        String result = author.getGivenFamily(true);
        assertEquals("Smith", result);
    }

    /**
     * Test Case 4: Abbr=True, GivenName=Missing, Suffix=Present. Expected: "Smith, Jr."
     */
    @Test
    void getGivenFamily_AbbrFullNameMissingWithSuffix() {
        Author author = createAuthor("", "", "Smith", "Jr.");
        String result = author.getGivenFamily(true);
        assertEquals("Smith, Jr.", result);
    }

    /**
     * Test Case 5: Abbr=False, GivenName=Present, Suffix=Missing. Expected: "John Smith"
     */
    @Test
    void getGivenFamily_FullNamePresentNoSuffix() {
        Author author = createAuthor("John", "J.", "Smith", null);
        String result = author.getGivenFamily(false);
        assertEquals("John Smith", result);
    }

    /**
     * Test Case 6: Abbr=False, GivenName=Present, Suffix=Present. Expected: "John Smith, Jr."
     */
    @Test
    void getGivenFamily_FullNamePresentWithSuffix() {
        Author author = createAuthor("John", "J.", "Smith", "Jr.");
        String result = author.getGivenFamily(false);
        assertEquals("John Smith, Jr.", result);
    }

    /**
     * Test Case 7: Abbr=False, GivenName=Missing, Suffix=Missing. Expected: "Smith"
     */
    @Test
    void getGivenFamily_FullNameMissingNoSuffix() {
        Author author = createAuthor("", "", "Smith", null);
        String result = author.getGivenFamily(false);
        assertEquals("Smith", result);
    }

    /**
     * Test Case 8: Abbr=False, GivenName=Missing, Suffix=Present. Expected: "Smith, Jr."
     */
    @Test
    void getGivenFamily_FullNameMissingWithSuffix() {
        Author author = createAuthor("", "", "Smith", "Jr.");
        String result = author.getGivenFamily(false);
        assertEquals("Smith, Jr.", result);
    }
}
```