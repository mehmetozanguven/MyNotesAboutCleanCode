# Clean Code - A Handbook of Agile Software Craftsmanship



## What is Clean Code?

- Elegant(zarif) and efficient code
- Make it hard for bugs to hide
- Pleasing(memnuniyet verici) to read
- Clean code does one thing
- Reading the clean code should make you smile the way well-designed car would
- Clean code shows us the problem that is trying to solve
- Code without tests is not clean, not matter how elegant it is, not matter how readable and accessible, if it has not tests, it be unclean
- Clean code always looks like it was written by someone who cares. There is nothing obvious that you can do to make it better
- Beautiful code makes the language look like it was made for the problem.
- Bad code **tempts(özendirmek)** the mess to grow.





## Meaningful Names

### 1. Use Intention-Revealing Names

- Names should reveal intent.
- Choosing good names takes time but saves more than it takes.

```java
int d; // elapsed time in days
```

- The name d reveals nothing. It does not evoke a sense of elapsed time nor of days
- Choose a name that specifies what is being measured and the unit of that measurement

```java
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```

- Choosing names that reveal intent can make it much easier to understand and change code.

```java
public List<int[]> getThem() {
	List<int[]> list1 = new ArrayList<int[]>();
	for (int[] x : theList)
		if (x[0] == 4)
		list1.add(x);
	return list1;
}
```

- Why is it hard to tell what this code is doing? There are no complex expressions. Spacing and indentation are reasonable and there are only 3 variables and 2 constants. They are just a list of arrays 
- The problem isn't the simplicity of the code but the implicity(in a way that is suggested but not communicated directly)
- The code implicitly requires that we know the answers to questions such as:
  - What kinds of things are in theList ?
  - What is the significance of the 0th subscript of an item in theList ?
  - What is the significance of the value 4 ?
  - How would I use the list being returned



### 2. Avoid Disinformation

- Programmers must avoid leaving false clues that obscure the meaning of code.
- For example let's say we have a class namely `XYZControllerForEfficientHandlingOfStrings`, after a while we created another class namely `XYZControllerForEfficientStorageOfStrings`  . The other developers may confuse to use the correct class because of the similarity between these classes



### Make Meaningful Distinctions

- Don' use such series: `(a1, a2, .. aN)` . They provide no clue to the author's intention

```java
public static void copyChars(char a1[], char a2[]) {
	for (int i = 0; i < a1.length; i++) {
	a2[i] = a1[i];
	}
}
```

- **Noise words are another meaningless distinction.** Imagine we have a `Product` class. If we have another called `ProductInfo` or `ProductData` we have made the names different without making them mean anything different. `Info` and `Data` are indistinct noise words like `a, an, the`
- Distinguish names in such a way that the reader known what the differences offer.



### Use Pronounceable Names

- We should make our names pronounceable.
- Bad example: `genymdhms` which means that (generation date, year, month, day, hour, minute and second)

```java
class DtaRcrd102{
    private Date genymdhsm;
    private Date modymdhsm;
    private final String psqint "102";
}
// convert to
class Customer{
    private Date generationTimestamp;
    private Date modificationTimestamp;
    private final String recordId = "102";
}
```

Intelligent conversation is now possible: “Hey, Mikey, take a look at this record! The generation timestamp is set to tomorrow’s date! How can that be?”



### Use Searchable Names

- Single-letter names can only be used  as local variables inside short methods (personal advice). The length of a name should correspond to the size of its scope. If a variable or constant might be seen or used in multiple places in a body of code, it is imperative to give it a search-friendly name.



### Avoid Encodings

- Don't use encoding for names



### Member prefixes

- Don't need to prefix member variables with `m_` anymore.
- Our classes and functions should be small enough that we don't need them.

```java
public class Part {
    private String m_dsc;
    
    void setName(String name){
        m_dsc = name;
    }
}
// -------------------------
public class Part{
    private String description;
    
    void setDescription(String description){
        this.description = description;
    }
}
```



### Interfaces and Implementations

- Prefix `I` is so common, but it gives many information to the users.
- We don't want users knowing that I am handing them an interface.
- For example, instead of `IShapeFactory & ShapeFactory` use `ShapeFactory & ShapeFactoryImpl`



### Class Names

- Classes and objects should have noun or noun phrase names like `Customer, WikiPage, Account, AddressParser`. Avoid words like `Manager, Processor, Data, Info` in the name of a class. A class name should not be a verb.

### Method Names

- Methods should have verb or verb phrase names like `postPayment, deletePage, save` 
- Accessors, mutators, and predicates should be named for their value and prefixed with `get, set, is` according to the javabean standard.

```java
string name = employee.getName();
customer.setName("mike");
if (paycheck.isPosted())...
```

- When constructors are overloaded, use static factory methods with names that describe the arguments. For example:

```java
Complex fulcrumPoint = Complex.FromRealNumber(23.0);
// is generally better than
Complext fulcrumPoint = new Complex(23.0);
```

- Consider enforcing their use by making the corresponding constructors private.



### Pick One Word per Concept

- Pick one word for one abstract concept and stick with it. For instance, it's confusing to have `fetch, retrieve  and get` as equivalent methods of different classes. Choose one of them for all.
- Likewise, it's confusing to have a `controller` and a `manager` and a `driver` in the same code base. What is the essential difference between a `DeviceManager` and a `ProtocolController` Why are both not `controller`s or both not `manager`s. The name leads us to expect 2 objects that have very different type as well as having different classes.



### Don't Pun

- Avoid using the same word for 2 purposes. Using the same term for 2 different ideas is essentially a pun.



#### Add Meaningful Context

- If we follow the "one word per concept" rule, we could end up with many classes that have, for example an `add` method. As long as the parameter lists and return values of the various `add` methods are semantically equivalent, all i s well.
- However one might decide to use the word `add` for "consistency" when he or she is not in fact adding in the same sense. For example let's say we have many classes where `add` will create a new value by adding or concatenating 2 existing values. Now let's say we are writing a new class that has a method that puts its single parameter into a collection. Should we call this method `add`? It might seem consistent because we have so many other `add` methods, but in this case, the semantics are different, so we should use a name like `insert` or `append` instead



### Use Solution Domain Names

- Use Computer Science terms, algorithm names, pattern names and so forth. Because the people who read our code will be programmers.
- Every programmer can understand for example `AccountVisitor` deals with Visitor pattern



### Use Problem Domain Names

- When there is no programmer-ease, use the name from the problem domain.



### Add meaningful Context

- We said that use well-named classes functions or namespaces. When all ese fails, then prefixing the name may be necessary as a last resort.
- Imagine that we have variables named `firstName, lastName, street, houseNumber, city, state and zipcode`. Taken together it's pretty clear that they form an address. 
- But what if we just saw the `state` variable being used alone in a method. Would we automatically infer that it was part of an address?
- We can add context by sing prefixes: `addrFirstname, addrLastName, addrState` and so on. At least readers will understand that these variables are part of a larger structure.
- Consider the method in the below. When we first look at the method, the meanings of the variables are opaque.

```javascript
private void printGuessStatistics(char candidate, int count) {
	String number;
	String verb;
	String pluralModifier;
	if (count == 0) {
		number = "no";
		verb = "are";
		pluralModifier = "s";
	} else if (count == 1) {
		number = "1";
		verb = "is";
		pluralModifier = "";
	} else {
		number = Integer.toString(count);
		verb = "are";
		pluralModifier = "s";
	}
	String guessMessage = String.format(
	"There %s %s %s%s", verb, number, candidate, pluralModifier
	);
	print(guessMessage);
}
```

- The function is a bit too long and the variables are used throughout. To split the function into smaller pieces we need to create a `GuessStaticticsMessage` class and make the three variables fields of this class. This provides a clear context for the three variables. They are definitively part of the `GuessStaticticsMessage`

```java
public class GuessStatisticsMessage {
	private String number;
	private String verb;
	private String pluralModifier;
	public String make(char candidate, int count) {
		createPluralDependentMessageParts(count);
		return String.format(
			"There %s %s %s%s",
			verb, number, candidate, pluralModifier );
	}
	private void createPluralDependentMessageParts(int count) {
		if (count == 0) {
			thereAreNoLetters();
		} else if (count == 1) {
			thereIsOneLetter();
		} else {
			thereAreManyLetters(count);
		}
	}
	private void thereAreManyLetters(int count) {
		number = Integer.toString(count);
		verb = "are";
		pluralModifier = "s";
	}
	private void thereIsOneLetter() {
		number = "1";
		verb = "is";
		pluralModifier = "";
	}
	private void thereAreNoLetters() {
		number = "no";
		verb = "are";
		pluralModifier = "s";
	}
}
```





### Don't Add Gratuitous(Unnecessary) Context

- In an imaginary application called "Gas Station Deluxe", it is a bad idea to prefix every class with `GSD`
- Likewise, say we invented a `MailingAddress` class in `GSD`'s accounting module, and we named it `GSDAccountAddress`. Later, we need a mailing address for our customer contact application. Do we use `GSDAcoountAddress` ?
- Shorter names are generally better than longer ones. 
- Add no more context to a name than is necessary



## Functions

- **The first rule of functions is that they should be small.**
- **The second rule of functions is that they should be smaller than that.** 
- Lines should not be 150 characters long.
- Functions should not be 100 lines long.
- Functions should hardly ever be 20 lines long

Here is the example:

```java
// code 1
public static String testableHtml(PageData pageData,boolean includeSuiteSetup) throws Exception {
		WikiPage wikiPage = pageData.getWikiPage();
		StringBuffer buffer = new StringBuffer();
		if (pageData.hasAttribute("Test")) {
			if (includeSuiteSetup) {
				WikiPage suiteSetup = PageCrawlerImpl.getInheritedPage( SuiteResponder.SUITE_SETUP_NAME, wikiPage);
		if (suiteSetup != null) {
			WikiPagePath pagePath =
			suiteSetup.getPageCrawler().getFullPath(suiteSetup);
			String pagePathName = PathParser.render(pagePath);
			buffer.append("!include -setup .").append(pagePathName).append("\n");
		}
	}
	WikiPage setup = PageCrawlerImpl.getInheritedPage("SetUp", wikiPage);
	if (setup != null) {
		WikiPagePath setupPath = wikiPage.getPageCrawler().getFullPath(setup);
		String setupPathName = PathParser.render(setupPath);
		buffer.append("!include -setup .").append(setupPathName).append("\n");
		}
	}
	buffer.append(pageData.getContent());
	if (pageData.hasAttribute("Test")) {
		WikiPage teardown = PageCrawlerImpl.getInheritedPage("TearDown", wikiPage);
	if (teardown != null) {
	 	WikiPagePath tearDownPath = wikiPage.getPageCrawler().getFullPath(teardown);
		String tearDownPathName = PathParser.render(tearDownPath);
		buffer.append("\n").append("!include -teardown .").append(tearDownPathName).append("\n");
    }
        // ... goes on
    pageData.setContent(buffer.toString());
	return pageData.getHtml();	
}

```

- Here is the refactored view:

```java
// code 2
public static String renderPageWithSetupsAndTeardowns(PageData pageData, boolean isSuite) throws Exception {
	boolean isTestPage = pageData.hasAttribute("Test");
	if (isTestPage) {
		WikiPage testPage = pageData.getWikiPage();
		StringBuffer newPageContent = new StringBuffer();
		includeSetupPages(testPage, newPageContent, isSuite);
		newPageContent.append(pageData.getContent());
		includeTeardownPages(testPage, newPageContent, isSuite);
		pageData.setContent(newPageContent.toString());
	}
	return pageData.getHtml();
}
```

- Here is the re-refactored view:

```java
// code 3
public static String renderPageWithSetupsAndTeardowns(PageData pageData, boolean isSuite) throws Exception {
	if (isTestPage(pageData))
		includeSetupAndTeardownPages(pageData, isSuite);
	return pageData.getHtml();
}
```

 

### Blocks and Indenting

- The above code implies that the blocks within `if, else, while, for ...`  statements and so on should be one line long. Probably **that line should be a function call**.
- Not only does this keep the enclosing function small, but is also adds documentary value because the function called within the block can have a nicely descriptive name.
- **This also implies that functions should be larger to hold nested structures. Therefore, the indent level of a function should not be greater than one or two.** This, of course, makes the functions easier to read and understand. 



### Do One Thing

- It should be very clear that code-1 is doing lots more than one thing. It's creating buffers, fetching pages, searching for inherited pages, rendering paths. 
- On the other hand, code-3 is doing one simple thing. It's including setups and teardowns into test pages.
- **Functions should do one thing. They should do it well. They should do it only**
  - The problem with this statement is that it is hard to know what **one thing** is.
  - Does code-3 do one thing? It's easy to make the case that it's doing three things:
    - Determining whether the page is a test page
    - If so, including setups and teardowns.
    - Rendering the page in HTML
  - Notice that the three steps of the function are one level of abstraction below the stated name of the function. We can describe the function by describing it as a brief paragraph:
    - TO RenderPageWithSetupsAndTeardowns, we check to see whether the page is a test page and if so, we include the setups and teardowns. In either case we render the page in HTML
- So, another way to know that a function is doing more than "one thing" is if we can extract another function from it with a name that merely(only) a restatement of its implementation.



### One Level of Abstraction per Function

- In order to make sure our functions are doing "one thing", we need to make sure that the statements within our functions are all at the same level of abstraction.
- Code-1 violates this rule. There are concepts in there that are at a very high level of abstraction, such as `getHtml()` others that are at an intermediate level of abstractions such as `String pagePathName = PathParser.render(pagePath)` and still others that are remarkably low level, such as ` .append("\n")`
- Mixing levels of abstraction within a function is always confusing.