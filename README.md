Static block Vs Static Method

Equals Override and Hashcode
String mutable what does it meant ?

between overriding and overloading a method.  explain the difference between an interface and an abstract class

they asked what a static block was.  they asked the difference between static variables and other variables.  

hey asked if java was pass by value or pass by reference
arrays and the like are passed by reference, primitives 
are passed by value

yes
c/c++ is both
i remember that for my C++ days in college :)


I usually get a stack vs heap question, but I misheard the question about static variables.  
I thought he said stack and I explained the difference between the stack and the heap.  
Then we figured out what happened and I went on to explain static vs non-static variables.
 

performance tuning
explain plan

AWR

Plat form service+ tools and framewwork + CAS

Intergrations - > MA associates + 

SOASCA - New Relic
Junit / Sonar cube / PMD check style

student {
int rollnum,
name
age
class
}

teacher {
int id,
name
age
list of class
}

class
{
list of student;
list of teachers;
Teacher classTeacher
}

class School
{
int schoolNum;
List of Class
List of Teachers
}


Controller:

StudentController.java
{
@Autowire StudentService
StudentService.saveStudent(student)

}

// Databse service should only be from DAO layer

StudentService.java
{
@Autowire StudentDAO

saveStudent(student)
{
// bussiness unit -like duplicate /already exists
StudentDAO
}
}

StudentDAO.java
{
SavaStudent(Student)
{
Fire insert queries;
}
}

####################

Inferface

AddPayment








price list

Pdp --> add to cart -- >
sku -- commerce item -- > Add to Order -- > list of commerce items

Reprice Order -- droplet or by FH
Pricing Engine -- > item price engine / shipping pricing engine / Tax pricing engine /Order pricing engine
Pricing Calculator -- sales price calculator / 
	market place item -- calulator customize
        gift card 

Shipping price -- > std / expedite /express  --- shipping price calculator
shipping discount calculator
Tax price calculator -- third party calculator
Order Price Calculator


--------- ATG Actor

CartModifierService   ----  CartModifierService extends CommerceServices {
TCCPaymentGroupManager  --- TCCPaymentGroupManager extends StorePaymentGroupManager implements Constants {
CheckOutService ---  CheckOutService extends CommerceServices {

eg : checkoutOut Actor
	<actor-chain id="saveOrder" transaction="TX_SUPPORTS">
		<component id="saveOrder" name="/com/tcc/commerce/checkout/CheckOutService" method-return-var="baseInfo" 
			invoke-method-requires-session-confirmation="false" 
			method="saveOrder" component-var="saveOrder" set-property-requires-session-confirmation="false">
			<input name="orderId" value="${param.orderId}" class-name="java.lang.String"/>
			<output id="baseInfo" name="baseInfo" value="${baseInfo}"/>
		</component>
	</actor-chain>
--  create commerce item

--  TCCOrderImpl order = (TCCOrderImpl) getPurchaseProcessConfiguration().getOrderManager().loadOrder(orderId);

----  PaymentTypeGroups 


 List<PaymentGroup> paymentTypeGroups = getPaymentGroupByType(order, ITEM_CASH);
        Cash cash = null;
        if (paymentTypeGroups.isEmpty()) {
            cash = (Cash) createPaymentGroup(ITEM_CASH);
            addPaymentGroupToOrder(order, cash);
            getOrderManager().addRemainingOrderAmountToPaymentGroup(order, cash.getId());
        } else {
        }
        recalculatePaymentGroupAmounts(order);
        cash.setTotalAmountPaid(amount);

	<actor-chain id="addDeviceItemToOrder" transaction="TX_SUPPORTS">
		<component id="addDeviceItemToOrder"
			name="/com/tcc/commerce/purchase/CartModifierService"
			method-return-var="baseInfo"
			invoke-method-requires-session-confirmation="false" method="addDeviceItemToOrder"
			component-var="baseInfo" set-property-requires-session-confirmation="false">
			<input name="losId" value="${param.losId}" class-name="java.lang.String" />
			<input name="deviceProductId" value="${param.deviceProductId}"
				class-name="java.lang.String" />
			<input name="type" value="${param.type}"
				class-name="java.lang.String" />
			<input name="additionalMsg" value="${param.additionalMsg}" 
				class-name="java.lang.String" />
			<output id="baseInfo" name="baseInfo" value="${baseInfo}" />
		</component>
	</actor-chain>

 			updateItemInOrder(deviceSkuId, isOrderedItem, configurableItem, order);
                        addDeviceInfoToOrder(contractType, activationType, configurableItem, deviceSkuId);

there is no FH or droplets, there is no gateway

Create New Repository :
$class=atg.adapter.gsa.GSARepository
$scope=global
repositoryName=MyNewRepository
definitionFiles=<YOUR_CONFIG_PATH>/<YOUR_XML_FILE_NAME>.xml
XMLToolsFactory=/atg/dynamo/service/xml/XMLToolsFactory
dataSource=/atg/dynamo/service/jdbc/JTDataSource
transactionManager=/atg/dynamo/transaction/TransactionManager
idGenerator=/atg/dynamo/service/IdGenerator

Repository - 

	type="primary"
 <table name="dcs_product" type="primary" id-column-name="product_id" shared-table-sequence="1">

	type="auxiliary"
 <table name="tcc_sku" id-column-name="sku_id" type="auxiliary" shared-table-sequence="1">


	type="multi"   --  keep the order
 <table name="tcc_sku_upc_code" type="multi" id-column-name="id" multi-column-name="sequence_num" shared-table-sequence="1">
         <property name="upcCode" column-name="upc_number" data-type="list" component-data-type="string" display-name="UPC Numbers" cache-mode="inherit" />
      </table>

NO Order

<table name="subjects_tbl" type="multi" id-column-names="id">
        <property name="favoriteSubjects" column-names="subject" data-type="set"
                  component-data-type="string"/>
    </table>


ATG Repository Cache Mode
ClientLockManager Component

If an SQL repository contains item descriptors that use locked caching, set the Repository component’s lockManager
property to a component of type atg.service.lockmanager.ClientLockManager. ATG provides a default ClientLockManager component:

/atg/dynamo/service/ClientLockManager

Thus, you can set an SQL Repository’s lockManager property as follows:

lockManager=/atg/dynamo/service/ClientLockManager
$class=atg.service.lockmanager.ClientLockManager
lockServerAddress=tartini.acme-widgets.com,corelli.acme-widgets.com
lockServerPort=9010,9010
useLockServer=true

