## Chapter 2: Meaningful Names
-  Avoid disinformation
	- Special meaning
		- Do not refer to a grouping of accounts as an `accountList` unless it’s actually a `List`. The word **list** means something specific to programmers
	- Beware of using names in small difference
		- XYZControllerForEfficient`Handling`OfStrings vs. XYZControllerForEfficient`Storage`OfStrings
- Make meaningful distinctions
	- No noise words
		- Product`Info` vs. Product`Data`
			- Info and Data have almost the same meaning
- Use pronounceable name
	- 使用读的出来的名称
- Use searchable names
	- 使用可搜索到名称
		- `5` vs `NumberOfTask = 5;`
		- `5` 难以搜索，`NumberOfTask` 容易搜索
- Class name
	- Classes and objects should have `noun` or `noun phrase` names
		- `Customer`, `WikiPage`, `Account`, and `AddressParser`
	- Avoid words like `Manager`, `Processor`, `Data`, or `Info` for the class name
	- A class name should **not** be a _verb_
- Method Names
	- Should be `verb` or `verb phrase` 
		- e.g. `postPayment`, `deletePage`, or `save`
- Constructors names
	- when constructors are overloaded, use `static factory methods` with names that **describe** the **arguments**
		- e.g. 
		``` java
		// Good
		Complex fulcrumPoint = Complex.FromRealNumber(23.0);
		// Bad
		Complex fulcrumPoint = new Complex(23.0);
		```
		- We can enfore using this way by making another constructor to `private`
- 每个概念对应一个词
	- Pick one word for one **abstract concept** and **stick** with it
		- e.g. `fetch`, `retrieve`, and `get` as **equivalent** methods of **different** classes
- 别用双关语

## Chapter 3: Functions
- 短小
	- 函数20行封顶最佳
- Do one thing
	- Functions should do **only one** thing
		- To see if a function is doing more than "one thing", is trying to extract another function from it
	- Function that do one thing **cannot** be reasonably divided into **multiple** sections
		- e.g. A function is divided into sections such as _declarations_, _initializations_, and _sieve_ --> 这就是函数做太多事的明显征兆
- One level of abstraction per function
	- 每个函数一个抽象层级
		- `getHtml()` 是**较高的**抽象层，`PathParser.render(pagePath)` 是**中间**抽象层，`.append("\n")` 是相当**低的**抽象层
	- Reading code __from Top to Bottom__
		- ``` java
			public static String render(PageData pageData, boolean isSuite) throws Exception {  
				return new SetupTeardownIncluder(pageData).render(isSuite);
			}
			
			private SetupTeardownIncluder(PageData pageData) {  	
				this.pageData = pageData;  
				testPage = pageData.getWikiPage();  
				pageCrawler = testPage.getPageCrawler(); newPageContent =  new StringBuffer();
			}
			
			private String render(boolean isSuite) throws Exception {  			
				 if (isTestPage())
					 includeSetupAndTeardownPages(); 
					 return pageData.getHtml();
				 }
			}
			```
- Switch statements
    - make sure each statement is low-level 
    - can be done by polymorphism
    - 不是很明白这一部分
    - e.g.
	    - ```java
		    public abstract class Employee {
			    public abstract boolean isPayday();
			    public abstract Money calculatePay();  
			    public abstract void deliverPay(Money pay);
		    }  
			-----------------  
			public interface EmployeeFactory {
				Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType; 
			}
			-----------------  
			public class EmployeeFactoryImpl implements EmployeeFactory {
				public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType { 
					switch (r.type) {
						case COMMISSIONED:  
							return new CommissionedEmployee(r) ;
						case HOURLY:  
							return new HourlyEmployee(r);
						case SALARIED:  
							return new SalariedEmploye(r);
						default:  
							throw new InvalidEmployeeType(r.type);
						}
					}
		  	}
			```
- Use descriptive names
- Function arguments
	- The ideal # of arguments for a function is **0**. Max is **3**
	- Flag arguments
		- Ugly
		- Solution
			- split the function into two: `renderForSuite()` and `renderForSingleTest()`
	- Dyadic function (两个参数的函数)
		- 尽量转化为一个参数的函数，哪怕多写一个函数，类似于 flag arguments 的处理方法
	- Triads (两个参数的函数)
		- need to think carefully before creating the triads
	- Argument objects
		- If a method needs more than 3 arguments, it means may need to be a `class`
	- Argument lists
		- for some reason, we need to pass a lot of variables --> can use `argument lists`
		- for example: 
			``` java
			void triad(String name, int count, Integer... args);
			```
	-	Verbs and keywords
		-	good name can express **meaning** of a function and the **order** of arguments
			``` java
			assertEqual(expected, actual);
			// --> 
			assertExpectedEqualsActual(expected, actual);
			```
	-	Have no side effects
		-	Be careful
			-	`!` your function promises to do **one** thing, but it also does other **hidden** things
	-	Output arguments
		-	Arguments are most naturally interpreted as **inputs** to a function
		-	If your function must change the `state` of something, have it change the state of its `owning object`
			-	`appendFooter(s)` --> `report.appendFooter()`
-	Command query separation
	-	return and setting should not do at the same time
		-	bad example
			-	```java
				public boolean set(String attribute, String value);
				// ...
				if (set("username", "unclebob") {...}
				```
		-	solution
			```java
			if (attributeExists("username")) {
				setAttribute("username", "unclebob");
			}
			```		
-	Prefer exceptions to returning error codes
	-	Extract `Try/Catch` blocks
		-	```java
			public void delete(Page page) { 
				try { // <-- try should be the first thing
					deletePageAndAllReferences(page);  // 隔离
				}
				catch (Exception e) { 
					logError(e);
				} 
			}
			
			// ---- 将 exception 开始隔离
			private void deletePageAndAllReferences(Page page) throws Exception { 
				deletePage(page);  
				registry.deleteReference(page.name); 	
				configKeys.deleteKey(page.name.makeKey());
			}

			private void logError(Exception e) { 
				logger.log(e.getMessage());
			}
			// ---- 隔离结束
			```
		-	Error handling is one thing
			-	Error handling function is only doing error handling
				-	if the keyword `try` exists in a function, it should be the **very first word** in the function
				-	if the keyword `catch/finally` exists in a function, it should be nothing afterwards
-	Structured Programming
	-	结构化编程
	-	How to
		1. code whatever you want to code
		2. write test cases and pass them
		3. refactor it
			- refine, split out, change names, eliminate duplication, shrink and reorder methods, break out

## Chapter 4: Comments
- Comments do not make up for bad code
	> Don’t comment bad code—rewrite it
	
- Explain yourself in code
	- Create a function that says the same thing as the comment you want to write
		- _"Check to see if the employee is eligible..."_ vs.
		- `isEligibleForFullBenefits();`
		``` java
		// bad example
		// Check to see if the employee is eligible for full benefits 
		if ((employee.flags & HOURLY_FLAG); 
		
		// good example
		if (employee.isEligibleForFullBenefits()); 
		```
- Comments must to write
	- Legal Comments (法律信息)
		- e.g. copyright
	- Informative Comments (提供信息的注释)
		``` java
		// format matched kk:mm:ss EEE, MMM dd, yyyy 
		Pattern timeMatcher = Pattern.compile(
			"\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*"
		);
		```
		- Explanation of Intent (对意图对解释)
			- 比如说你写这段函数对意义是什么
				- 个人觉得这是最常见对用法之一
		- Clarification 
			1. Unreadable code --> easy to understand
			2. Or, for some unchangeable code
				- e.g. library code
				``` java
				// a < b
				assertTrue(a.compareTo(b) == -1); // <-- lib code
				```
		- Warning
		- TODO
			- explains **why** the function has a current implementation 
			- what that function’s **future** should be
		- Javadocs in Public APIs
- Bad comments
	- Redundant comments
	- Misleading comments
	- Mandated comments (循规式注释)
		- e.g. `Javadoc` and every variable must have a comment
			``` java
			/**
			 * xxxxxxxxxxx
			 * @param title The title of the CD    
			 * @param author The author of the CD    
			 */
			```
	- Noise comments (废话注释)
		``` java
		/**  
		 * Returns the day of the month.  
		 * @return the day of the month. 
		 */
		public int getDayOfMonth() { 
			return dayOfMonth;
		}
		```
	- Don't use a comment when you can use a function or a variable

## Chapter 5: Formatting
- Vertical formatting 
	- 紧密相关对代码应该互相靠近
	- 关系密切对概念应该相互靠近
	- variable declarations
		- should appear at the **top** of each function
		- or, just before a `loop`
	- dependent functions (相关函数)
		- caller should be **above** the callee 
- Horizontal formatting

## Chapter 6: Objects and Data Structures
- Data Abstraction
	- 将`数据`抽象
	- 我的理解是，当我们需要想要将`数据结构`隐藏起来的时候，要注意，可能 `method` 也会将其暴露
		- e.g. 
		```java
		public interface Vehicle {  
			double getFuelTankCapacityInGallons(); 
			double getGallonsOfGasoline();
		}
		```
		vs.
		```java
		public interface Vehicle {
			double getPercentFuelRemaining();
		}
		```
		- Second one is better，因为第一个里面是两个 `getter` 来拿到两个 `variable`: `fuelTankCapacityInGallons` and `gallonsOfGasoline`.  It exposed definition of these two variables. Compared to the `getPercentFuelRemaining()`, user has no idea 谁除以谁, it saves variables from exposing. 
	> We do not want to expose the details of our data.
	> Serious thought needs to be put into the best way to represent the data that an object contains. The worst option is to blithely add getters and setters 

- Date/Object Anti-Symmetry
  - OO code vs. procedural code
  - 面向对象较难的事，对于过程式代码却较容易，反之亦然
  - We need to consider when should use OOD code, when should use procedural code
- The Law of Demeter
  - > 模块不应了解它所操作对象的内部情形
  - Train Wrecks 
    - 个人理解为类似于 链式 的表达式
    - 第二种方式更好
    - 思考
      - 在我平时写代码的时候，可能会用到 function progarmming 的 chain，这个和此问题是不一样的，不要混淆
      - 尽量不要用这种 accessor 的 chain
	``` java
	final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();

	// vs.
	final String outputDir = ctxt.options.scratchDir.absolutePath
	```
  - Hybrids
    - Do not create a class with half object and half data structure
  - Hidden Structure
    - 没看懂
- Data Transfer Objects (DTO)
  - 