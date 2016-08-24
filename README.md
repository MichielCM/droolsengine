# Synopsis
A convenience implementation of Drools 6.4.x, facilitating creation of knowledge sessions from a variety of rule sources, adding and retrieving objects to and from sessions, executing rules, and handling global variables.

Supports intitializing knowledge session from:
- DRL files containing rules in Drools' MVEL format;
- DRL Strings containing rules in Drools' MVEL format;
- CSV Strings containing rules in Drools' decision table format;
- XLS Byte[] containing rules in Drools' decision table format.

#Sample Code
This example shows how to create a session from an array of strings, run the rules, and retrieve an array of MyPOJO objects. Chaining is supported for clarity of coding.
```
MyPOJO[] results = new DroolsEngine(
	ResourceType.DRL,
	new String[] {
		"rule \"HelloWorld\" when $pojo : MyPOJO(foo.isEmpty()) then $pojo.foo = \"bar\" end"
	}
).add(
	new MyPOJO[] {
		myFirstPOJO, mySecondPOJO
	}
).execute().get(
	MyPOJO.class
);
```
DroolsEngine can be initialized from Excel files (XLS) provided as an array of byte arrays (Byte[][]):
```
Byte[] excelFile;

new RuleEngine(
	ResourceType.XLS,
	new Byte[] {
		excelFile
	}
)
```
