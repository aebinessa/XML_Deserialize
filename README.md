# XML_Deserialize

To build the automation process for extracting and displaying exchange rates from an XML file, follow these steps:

### Open Studio and create a new Process.
 - Drag a Sequence container into the Workflow Designer.
 - Next, create the following variables:

 - XML of type String	
 - XMLDeserialized of type	XDocument	
 - XMLXpathResult of type	Object	
 - XMLNodes	of type IEnumerable<XNode>	
 - XMLAttributes of type IEnumerable<XAttribute>	
 - AllExchangeRates	of type String

### next:
   
 - Add a Read Text File activity within the sequence.
 - Set the File Name field to "daily_usd.xml".
 - Assign the XML variable to the Content field.
 - Add a Deserialize XML activity after the "Read Text File" activity.
### next:
 - Set XML in the XML String field.
 - Assign XMLDeserialized to the XMLDocument field.
 - Add an Execute XPath activity following the "Deserialize XML" activity.
### next:
 - Set XMLDeserialized in the Existing XML field.
 - Use the expression "string(/channel/lastBuildDate)" in the XPath Expression field.
 - Assign XMLXpathResult to the Result field.
 - Add a Message Box activity after the "Execute XPath" activity.

 - Use the expression "Exchange rates for " + XMLXpathResult.ToString in the Text field.
 - Add a Get XML Nodes activity next.

 - Set XMLDeserialized in the ExistingXML field.
 - Assign XMLNodes to the XMLNodes field.
 - Add a Get XML Node Attributes activity after the "Get XML Nodes" activity.
### next: 
 - Set XMLNodes(0) in the Existing XML Node field.
 - Assign XMLAttributes to the Attributes field.
 - Add another Message Box activity after the "Get XML Node Attributes" activity.

 - Use the expression XMLAttributes(0).Name.ToString + ": " + XMLAttributes(0).Value.ToString in the Text field.
 - Add an Assign activity next.
### next:
 - Set AllExchangeRates in the To field.
 - Use the expression "Exchange Rates" + System.Environment.NewLine in the Value field.
 - Add a For Each activity.
### next: 
 - In the Values field, use the expression XMLDeserialized.Element("channel").Elements("item").
 - Select System.Xml.Linq.XElement from the TypeArgument drop-down list.
 - Inside the "For Each" container, add an Assign activity.
### finally: 
 - Set AllExchangeRates in the To field.
 - Use this expression in the Value field: AllExchangeRates + System.Environment.NewLine + "1 " + currentXElement.Element("baseName").Value.ToString + " = " + currentXElement.Element("exchangeRate").Value.ToString + " " + currentXElement.Element("targetName").Value.ToString.
And now, add a Message Box activity after the "For Each" activity.

 After that, Set allExchRates in the Text field.

 And with that you are done.

 ![image](https://github.com/user-attachments/assets/b07e92c3-931a-4f58-9ba2-5d4c7801c5b7)
 ![image](https://github.com/user-attachments/assets/b5f90222-ab9a-4908-a308-2e92ef4dff9e)


 Credits to : https://docs.uipath.com/activities/other/latest/developer/read-and-deserialize-a-xml-file


