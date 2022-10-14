# Week 3 Lab Report
## Part 1 **searchEngine.java**
```
class Handler implements URLHandler {
    List<String> str = new ArrayList<String>();
    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("String: %s", str);
        }

        else if (url.getPath().equals("/add")) {
            String[] parameters = url.getQuery().split("=");
            str.add(parameters[1]);
            return String.format("String %s added!", parameters[1]);
        } else {
            if (url.getPath().contains("/search")) {
                List<String> str2 = new ArrayList<String>();
                String[] parameters = url.getQuery().split("=");
                for (String s : str) {
                    if (s.contains(parameters[1])) {
                        str2.add(s);
                    }
                }
                String comma = ",";
                String finalStr = String.join(comma, str2);
                return finalStr;
            }
            return "404 Not Found!";
        }
    }
}
```

* The first screenshot shown below is the base path that will appear when you first run the website. The code will bring you to a homepage where it shows you the string list. This is the first if statement in the code block above and it will check for the `"/"` path and return the string list variable `str`. in the format of `String: str`

![Image](screenshots/searchBase.png)

* The next three screenshots are tests for the add method for my website. This method is the `else if` statement in the code snippet above. First the code will check a `/add` path and then check for query `?s` spliting the `"="` into a parameters string array. The parameters string array will have 2 values with `parameters[0] = s` and `parameters[1] = the string you are added`. Then our original string list will add `parameters[1]` and return  that `parameters[1]` has been added.
![Image](screenshots/searchadd1.png)
![Image](screenshots/searchadd2.png)
![Image](screenshots/searchadd3.png)

* The screenshot show below is the test for the search method. The search method is the `else` statement in the code block above. First the code will check for the `/search` and then initialize a new temporary string list `str2`. Then we will check for query `?s` spliting the `"="` into a parameters string array. The parameters string array will have 2 values with `parameters[0] = s` and `parameters[1] = substring we are searching for`. Then we use a for loop to iterate `str` into `String s` and we check to see if the `string s` contains the `parameters[1]` which is the substring we are looking for. If the string does contain the substring we add it into the temporary list string we iniaitlized earlier `str2`. We then combine `comma` and `str2` by using `String.join(comma, str2)` and return this as a string.
![Image](screenshots/searchSearch.png)
* The error message in the last line of code appears when neither search or add is called.

## Part 2 (Bug Searching)
### **ArrayExamples: averageWithoutLowest**
* The first bug that I am choosing for my lab report would be the averageWithoutLowest function in the ArrayExamples file.
* This is the original failure inducing input that I tested using an array with (0.2, 1, 5, 6, 0.7) as my first test and an empty array as my second test. ![Image](screenshots/ArrayTest.png)
* Running the test I got the symptons in the image below which says that it expected the value of 2.54 but instead returned 3.175. ![Image](screenshots/ArraySymptons.png)
* Looking at the code I realized the that bug was in the return statement.The code was `return sum / (arr.length -1)` when it should have been ` return sum / arr.length`. ![Image](screenshots/ArrayCode.png)
* The connection between the sympton and the bug is that the sympton is looking for the average of the array without the lowest number; however,in the bug it is taking the average of the array without factoring in the fact that the lowest number is still an element in the array. The sympton is looking for `sum/arr.length` while the bug is outputing `sum/(arr.length - 1)`.
* This bug causes this sympton for this particular input because the input will sum into `12.7` which divided by `arr.length` is the equate to `2.54`; however, the bug is `sum/(arr.length-1)` which means it is taking the average of one less element of the array which causes the sympton of `3.175`.

###  **ListExamples: merge**
* The second bug that I am choosing for my lab report would be the merge function in the ListExamples file.
* This is the original failure inducing input that I tested using a string list with inputs (` "physics" `, ` "math" `,` "biology" `) ![Image](screenshots/ListTest.png)
* Running the test I got the symptons in the image below which says that it expected the array `[physics, biology]` and it returned `[biology, phyiscs]`. ![Image](screenshots/ListSymptons.png)
* Looking at the code I realized that the problem lay in the line where it said `result.add(index: 0, s)`. Instead of putting the array back in the same order the code was reversing the array after checking the string. The fix I implemented was replacing the code with `result.add(s)` as shown in the image below. ![Image](screenshots/ListFilter.png)
* The sympton was looking for the original array in the same order with strings that did not have `i` removed. On the other hand, the bug was outputing the original array in reverse order with strings that did not have `i`. 
* This bug causes this sympton for this particular input because the function will filter out the `math` string becuase it does not contain the string `s` and then make a place the strings that do containt `s` into the array result. The problem is that it adds the string into index 0 which will essentially reverse the array. This bug would affect every single type of input and give the same sympton of reversing the array each time.