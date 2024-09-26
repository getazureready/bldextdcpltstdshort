# Lab 01: Creating and using Copilot from Copilot Studio for managing a Real Estate Application

**Lab Duration** – 120 minutes

**Introduction**

Contoso Real Estate specializes in the sale and management of both
commercial and residential properties. Currently, customer information
is efficiently stored within their Dataverse instance, allowing for
streamlined data management. However, the booking process presents a
significant challenge.

At present, customers can only request bookings via phone, leading to an
overwhelmed phone line and long wait times. This situation not only
frustrates customers but also risks losing potential business as many
are unable to connect with the office to request services.

To address these issues, Contoso Real Estate is committed to developing
a comprehensive digital solution. This solution will empower customers
to easily access information about the booking process and submit
booking requests online.

**Objectives**

- Build a standalone copilot for Contoso Real Estates from Copilot
  Studio (that will allow customers to discover information about the
  real estate booking process and create booking requests for the office
  to review.)

- Create Topics to set up the logic of the bookings.

- Create the Dataverse tables required for the bookings.

- Publish the copilot.

- Configure the Dynamics 365 workspace and connect the copilot to it.

- Implement entities, slot filling and variables usage in the Copilot for
Real Estate app. Enhance the copilot created for the Real Estate app to
elevate the customer experience by implementing Generative AI.



## Exercise 0: Setting up your environment

### Task 1: Login to VM

1.	Login to the VM using the **Username** and **Password** from the **Resources** tab.
   
    ![](./media/Picture1.png)
  	
### Task 2: Synchronize the VM clock

1.	After logging into the VM, right click on the clock at the bottom right corner of the screen.
   
2.	Select **Adjust date and time**.
   
    ![](./media/picture2.png)
  	
3.	On the Settings screen that opens up, click on **Sync now** under Additional settings.

    ![](./media/picture3.png)
 
4.	This takes care of synchronizing the time just in case the automatic synchronization does not work.
 
5.	**Close** the Settings pane.

    ![](./media/picture4.png)
 

## Exercise 1: Setting up the Dynamics 365 Customer Service

### Task 1: Sign up for Dynamics 365 Customer Service trial

1.  Login to
    +++https://dynamics.microsoft.com/en-us/customer-service/overview/+++.
    
2.	Login using the **Office 365 Tenant details** from the **Resources** tab if prompted.

    ![](./media/im01.png)
  	
3.  Click on **Try for free**

    ![](./media/image1.png)

4.	Enter your **Office 365 Administrative Username** from the **Resources** tab, select the check box and click on **Start your free trial**.

    ![](./media/image2.png)

6.  Enter the region as **United States**, enter your **Phone number**
    and click on **Submit**.

    ![](./media/image3.png)

7.  The **Dynamics 365 Customer Service workspace** opens.

  ![](./media/image4.png)

5.  Click on Customer Service workspace to open the **Apps**.

  ![](./media/image5.png)

6.  Click on **Customer Service admin center** to open it.

    ![](./media/image6.png)

7.  Select **Routing** under **Customer Support** group.

    ![](./media/image7.png)

8.  On the **Routing** page, under **Record routing**, click **Manage**
    next to **Turn on Unified Routing for Records**.

    ![](./media/image8.png)

9.  On the **Service Configuration Settings** page under **Unified
    routing**, make sure that the **Turn on unified routing** toggle is
    set to **Yes**.

    >[!Note] **Note**: The **Turn on unified routing** toggle is set to **Yes** only
if consent is already provided by the tenant administrator.

10. Click **Save**.

    ![](./media/image9.png)

### Task 2: Configure Omnichannel Power Virtual Agent Extension

1.  Open the link,
    +++https://appsource.microsoft.com/en-cy/product/dynamics-365/mscrm.omnichannelpvaextension?tab=Overview&ref=dynamicsforcrm.com+++
    and click on Get it now in the Omnichannel Power Virtual Agent
    Extension page.

    ![](./media/image16.png)

    ![](./media/image17.png)

2.  Select the **CustomerService Trial** under **Select an environment**, select the check boxes 
    and click on **Install**.

    ![](./media/image18.png)

3.  In the Dynamics 365 apps page, click on the entries that shows
    **Update available**, **select** the **check box** to agree to the
    terms and click on **Update**.

    Make sure to do this for **all** the entries with **Update available**
    as the Status.

    ![](./media/image19.png)

    ![](./media/image20.png)

### Task 3: Configure search settings in the Power Platform admin center

1.  Login to +++https://admin.powerplatform.microsoft.com/+++ using
    your tenant details. Select **Environments** -> **CustomerService
    Trial**.

    ![](./media/image21.png)

2.  Select the drop down next to **Resource** (in the top pane) and
    select **Dynamics 365 apps**.

    ![](./media/image22.png)

3.  Make sure that **Omnichannel for Customer Service** is
    **Installed**.

    ![](./media/image23.png)

4.  Navigate back to the **Environments -\> CustomerService** **Trial**
    page in the admin center. Select **Settings** from the top pane.

    ![](./media/image24.png)

5.  Select **Product** -\> **Features**.

    ![](./media/image25.png)

6.  Toggle **Dataverse Search** and **Single table search** option to
    **ON.**

    ![](./media/image26.png)

    Scroll down and click on the **Save** button at the bottom right.

    ![](./media/image27.png)

## Exercise 2: Setting up Power Apps and Dataverse

### Task 1: Sign up for the Microsoft Power Apps Developer Plan

1.  Navigate to +++https://powerapps.microsoft.com/free/+++ and select
    **Start free**.

    ![](./media/image28.png)

2.  Under **Let's get started**, enter the **tenant id** in the
    text box, check the agreement box and select **Start free**.

    ![](./media/image29.png)

3.  If you see a prompt that you have an existing account with
    Microsoft. Select **Sign in**. Enter your password.

4.  If prompted, Select **Yes** to stay signed in.

5.  Click on **Environment** in the top-right corner of the screen and
    select **CustomerService Trial**.

    ![](./media/image30.png)

### Task 2: Create a solution

1.  From the Power Apps Maker
    Portal +++https://make.powerapps.com/+++, select **Solutions**
    form the left pane.

    ![](./media/image31.png)

2.  Click on **+ New solution**.

    ![](./media/image32.png)

3.  Enter +++**Bookings**+++ for the Display name and click on **+ New
    publisher**.

    ![](./media/image33.png)

4.  Enter the below details and then click on **Save**.

    | **Property**     | **Value**     |
    |------------------|---------------|
    | **Display name** | +++Contoso+++ |
    | **Name**         | +++contoso+++ |
    | **Prefix**       | +++contoso+++ |

    ![](./media/image34.png)

5.  Select **Contoso (contoso)** under Publisher and then click on
    **Create**.

    ![](./media/image35.png)

6.  Select **Back to solutions** in the top-left of the screen.

    ![](./media/image36.png)

### Task 3: Set the preferred solution

1.  Under Solutions in the Maker portal, select **Manage** for **Set
    your preferred solution**.

    ![](./media/image37.png)

2.  Select **Bookings (contoso)** under **Unless otherwise specified,
    save my changes in** and select **Apply**.

    ![](./media/image38.png)

    ![](./media/image39.png)

### Task 4: Create the Real Estate Properties custom table

Follow these steps to create a new custom table in Dataverse for Real
Estate Properties.

1.  From the left navigation pane, select **Tables**, select the drop down next to + New table and then select **Create new tables (preview)**.

    ![](./media/picture5.png)

2.	On the Create new tables (preview) screen, click on **+ New table -> Add columns and data**.
   
    ![](./media/picture6.png)
  	
3.  Rename the table from **Table** to +++**Real Estate Property**+++ and then click on **Save and exit**.

    ![](./media/picture7.png)

4.	Once saved, click on **Custom** to find the newly created table there. Click on the **Real Estate Property** table.

     ![](./media/picture8.png)
   
5.	Under the **Real Estate Property columns and data**, change the name of the column called **New Column** (Click on the drop down next to **New Column** and select **Edit Column** and update the **Display name**) to +++**Property Name**+++.

    ![](./media/image42.png)

6.	Select the **+** button to add a new column in the columns and data pane. In the New column pane, enter the following values, and then select **Save**.

      - Display name: +++**Asking Price**+++
  
      - Data type: Currency

    ![](./media/im2.png)
  	
    ![](./media/im3.png)

7.  Add the following two columns.

    | **Display name** | **Data type**                                   |
    |------------------|-------------------------------------------------|
    | +++Street+++     | Single line of text (this value is the default) |
    | +++City+++       | Single line of text (this value is the default) |

8.  Add another column with the below values

    - **Display name**: +++Bedrooms+++
  
    - **Data type**: Choice -> Choice

      ![](./media/im5.png)
      
    Create the choice values:

    Select **+ New choice** under **Sync this choice with** option

    ![](./media/im06.png)

    - Under **Choices**, provide the **Display name** as +++**Bedrooms**+++.
    - You see two entry fields titled **Label** and **Value**. Enter **1** under the label. Power
    Apps assigns a value automatically but you can change the value
    to **1**.

    - Select **+ New choice** and make **2** the new entry for Label
  and **2** for Value.

  - Select **+ New choice** and make **3** the new entry for Label
  and **3** for Value.

  - Select **+ New choice** and make **4** the new entry for Label
  and **4** for Value.

  - Select **+ New choice** and make **5** the new entry for Label
  and **5** for Value.

  - Select **Save**.

  ![](./media/im6.png)

  Select the added choice **Bedrooms**, by clicking the drop down of **Sync this choice with**

  ![](./media/im7.png)

  Click on **Save**.

  ![](./media/im07.png)
  
9.  Select the **+** button to add a new column in the
    columns and data pane.

10.  In the New column pane, enter the following values, and then
    select **Save**:

    - **Display name**: +++Bathrooms+++

    - **Data type**: Choice -> Choice

        ![](./media/im8.png)

  **Note:** Repeat the step 8 process with the Value **Bathrooms**.

  Create the choice values
  
    -  Under **Choices**, provide the Display name as +++Bathrooms+++.
    
    -  You see two entry fields titled **Label** and **Value**. Enter **1** under the label. Power Apps assigns a value automatically but you can change it to **1**.
  
    - Select **+ New choice** and make **2** the new entry for Label
    and **2** for Value.
  
    - Select **+ New choice** and make **3** the new entry for Label
    and **3** for Value.
  
    - Select **+ New choice** and make **4** the new entry for Label
    and **4** for Value.
  
    - Select **+ New choice** and make **5** the new entry for Label
    and **5** for Value.
  
    - Select **Save**.

    ![](./media/im9.png)

    Select the created choice and click on **Save** in the column addition pane.

    ![](./media/im10.png)
    
11.  Add another column by selecting the **+** button again in the columns and data pane.

  In the New column pane, enter the following values, and then
select **Save**:

  - **Display name**: +++**Client**+++
  
  - **Data type**: Lookup -> Lookup
  
  - **Related Table**: Contact

    ![](./media/im11.png)

13. Once the columns are created, under **Real Estate Property columns and
    data**, enter the following test data:

    >[!Note] **Note:** If the required columns are not getting displayed, adjust the columns that are displayed by selecting the **+<number>more**
    >
    >![](./media/im12.png)
    
    - Property Name: +++**1100 High Villas**+++

    - Asking Price: +++**250,000**+++

    - Bathrooms: **3**

    - Bedrooms: **2**

    - City: +++**Redmond**+++

    - Street: +++**Main Avenue**+++

    - Client: **Select any contact**

      ![](./media/image48.png)

### Task 5: Create the Bookings table

Follow these steps to create a new custom table in Dataverse for Real
Estate Property Bookings.

1.	From the left navigation pane, select **Tables**, select the **drop down** next to **+ New table** and then select **Create new tables (preview)**.

    ![](./media/picture5.png)

2.	On the Create new tables (preview) screen, click on **+ New table -> Add columns and data**.
   
    ![](./media/picture6.png)
  	
3.  Rename the table from **Table** to +++**Booking Request**+++ and then click on Save and exit.

    ![](./media/picture10.png)

4.	Once saved, click on **Custom** to find the newly created table there. Click on the **Booking Request** table.

   ![](./media/picture11.png)

5.	Under the **Booking Request columns and data**, Change the name of the column called **New Column** to +++**Booking Name**+++.

    ![](./media/image51.png)

6.  Create the following columns with the name and data type as
    specified in the table below. Select **Save**.

     -  Display name – +++**Property**+++
     -  Data type – **Lookup** -> **Lookup**
     -  Related Table – **Real Estate Property**

      ![](./media/image52.png) 
    
      -  Display name – +++**Viewer Name**+++
      -  Data type – **Single line of text**
    
      -  Display name – +++**Viewer Email**+++
      -  Data type – **Single line of text**
      -  Format – **Email**
  
      -  Display name – +++**Booking Date**+++
      -  Data type – **Date and time**
   
      -  Display name – +++**Notes**+++
      -  Data type – **Multiple lines of text**

      ![](./media/image53.png)
   
      ![](./media/image54.png)

7.  Add a choice data type column with the below details.
        
      -  Display name – +++**Decision**+++
      -  Data type – **Choice -> Choice**
    
          ![](./media/im012.png)
         
    Click on **+ New Choice – Display name** – +++Decision+++, enter the below details and click on **Save**.
    
     - Label – +++**Undecided**+++
            
     - Value – 1
            
     - Label – +++**Accepted**+++
            
     - Value – 2
            
     - Label – +++**Declined**+++
            
     - Value – 3

      ![](./media/im14.png)

    Select the added Choice **Decision**, designate **Undecided** as the **Default choice** and click on **Save**.
    
    ![](./media/im13.png)

    ![](./media/image55.png)

## Exercise 3: Working with Copilot Studio

### Task 1: Sign up for Copilot Studio trial

1.  Open the url +++https://copilotstudio.microsoft.com/+++.

2.  Leave the **Choose your country/region** with the **default** value
    and click on **Get Started**.

    ![](./media/image57.png)

3.  Click on **Environments** on the top left and select
    **CustomerService Trial**.

    ![](./media/image58.png)

4.  Select **Skip** if you get a Welcome to Copilot Studio! Prompt.

    ![](./media/image59.png)

### Task 2: Create the Real Estate Booking Service Copilot

1.  Select **Create** from the left navigation pane and select the **New
    copilot** tile.

    ![](./media/image60.png)

2.  Select **Skip to configure**.

    ![](./media/image61.png)

3.  Fill in the below details.

    - Name - +++**Real Estate Booking Service**+++
    
    - Description - +++**Create bookings for real estate properties**+++
    
    - Instructions - +++**Create a copilot for topics relating to creating
      bookings for real estate properties+++**
    
    - Language **–** Select **English**

    ![](./media/image62.png)

4.  Select the three dots next to the Create button in the top-right of
    the screen and select **Edit advanced settings**.

     ![](./media/image63.png)

5.  Select the **Bookings** solution and select **Save**.

     ![](./media/image64.png)

6.  In the top-right of the screen, select **Create**.

     ![](./media/image65.png)

7.  Once the copilot is created, in the Test your copilot pane, enter
    +++**How do I make a booking?**+++ and click **Enter** and observe the
    response.

    ![](./media/image66.png)

### Task 3: Configure Security

1.  Select **Settings** in the top-right of the screen.

    ![](./media/image67.png)

2.  Select the **Security** tab and then select
    the **Authentication** tile.

    ![](./media/image68.png)

3.  Select **No authentication** and click on **Save**.

    ![](./media/image69.png)

4.  Select **Save** in the **Save this configuration** prompt.

    ![](./media/image70.png)

5.  Once the Authentication settings are saved, click on the **Close**
    option to close the **Settings** pane.

    ![](./media/image71.png)

### Task 4: Remove topics

Sample topics are included with new copilots. Remove these sample
topics. Disable system topics that you don't require.

1.  Select the **Topics** tab from the top menu of the Copilot Overview
    page.

    ![](./media/image72.png)

2.  You will land in the **Custom** Topics page.

3.  Select the **three dots** next to the **Lesson 1** topic and select
    **Delete**.

    ![](./media/image73.png)

4.  Select **Delete** in the confirmation window.

    ![](./media/image74.png)

5.  Repeat the delete for Lesson 2 and Lesson 3.

    ![](./media/image75.png)

    ![](./media/image76.png)

6.  Select the **System** tab. Toggle **Enabled** to **Off** for the
    **Sign in** topic.

    ![](./media/image77.png)

### Task 5: Publish and test the copilot

1.  Select **Publish** and select **Publish** again.

    ![](./media/image78.png)

2.  Select **Publish** in the **Publish this copilot** dialog.

    ![](./media/image79.png)

### Task 6: Demo Website

The Demo website allows users without a license to test your copilot.
You can provide them with the URL to the demo website.

1.  Select the **three dots** next to the **Settings** button in the
    top-right of the screen and select **Go to demo website**.

    ![](./media/image80.png)

2.  In the **Type your message** text box, enter +++**What information is needed to book a viewing for a real estate property?**+++ and observe the response from the copilot.

    ![](./media/image81.png)

## Exercise 4: Create and manage topics using Copilot

### Task 1: Create a topic using Copilot

Topics can be created and edited using natural language.

1.  Select your copilot, **Real Estate Booking Service** in the Copilot
    pane on the left-hand side of the Copilot Studio.

    ![](./media/image82.png)

2.  Select the **Topics** tab. Select **Add a topic** and select
    **Create from description with Copilot**.

    ![](./media/image83.png)

3.  Enter the below details and click on **Create**.

    - Name your topic - +++**Customer Details**+++
    
    - Create a topic to... - +++**Ask the customer for their name and email
      address**+++

      ![](./media/image84.png)

4.  A new topic displays with the generated trigger phrases and question
    nodes.

5.  Select **Save**.

    ![](./media/image85.png)

### Task 2: Update nodes with natural language

1.  If the **Edit with copilot** pane isn't shown on the right-hand side
    of the screen, select the **Copilot** icon in the upper part of the
    authoring canvas.

2.  Select the second question node, **What is your email address?**

3.  In the **Edit with Copilot** panel, in the **What do you want to
    do?** field, enter the following text:

    +++**Update the message in this question node to say thank you to the Name variable from the previous node and then proceed to ask the email address question**+++

4.  Select **Update**.

    ![](./media/image86.png)

5.  Select **Save**.

    ![](./media/image87.png)

### Task 3: Add nodes with natural language

In addition to adding updating existing nodes, you can use Copilot to
add new ones.

1.  Make sure that no node is selected by clicking in the empty space
    around the nodes.

2.  In the **What do you want to do?** field, enter the following text
    and then select **Update.**

    +++**Add a new multiple-choice question to prompt the user if the details are correct with two options Yes or No**+++

    ![](./media/image92.png)

3. A new question node is added to the end of the topic with options
    for the user to select.

4. Select **Save**.

    ![](./media/image93.png)

### Task 4: Configure the scope of the variables

1.  Select **Variables** to open the Variables pane.

    ![](./media/image94.png)

2.  Select the right-hand check boxes for the topic variables and click
    on **Save**.

    ![](./media/image95.png)

## Exercise 5: Create and manage topics manually

### Task 1: Create a topic from blank

1.  Select the **Topics** tab.

2.  Select **Add a topic** and select **From blank**.

    ![](./media/image96.png)

3.  Select **Details** to open the Topic details dialog.

    ![](./media/image97.png)

4.  Fill in the below details and click on **Save**.

    - **Name** - +++Book a Real Estate Showing+++
    
    - **Display Name –** +++**Book**+++
    
    - **Description**  - +++Select the property and requested date and
      create a booking request+++

    ![](./media/image98.png)

5.  Select **Details** to close the Topic details dialog.

    ![](./media/image99.png)

### Task 2: Add trigger phrases

1.  Select **Edit** under **Phrases** in the **Trigger**. Enter +++**I
    want to book a real estate showing**+++ under **Add Phrases** and
    select the **+** icon.

    ![](./media/image100.png)

2.  Enter the below phrases one by one.

  - +++**Schedule a real estate showing**+++
  
  - +++**Arrange the viewing for a real estate property**+++
  
  - +++**Set up an appointment to view a house**+++
  
  - +++**Plan a property viewing**+++

3.  Once all the phrases are added, select **Save**.

    ![](./media/image101.png)

### Task 3: Add a message node

1.  Select the **+** icon under the Trigger node and select **Send a
    message**.

    ![](./media/image102.png)

2.  In the **Enter a message** field, enter the following text:

    +++Hi, I can help you with booking a real estate property showing.+++

3.  Select **Save**.

    ![](./media/image103.png)

### Task 4: Add a Topic management node

1.  Select the the **+** icon under the send a message node and
    select **Topic management -\> Go to another topic**.

    ![](./media/image104.png)

2.  Select the **Customer Details** topic.

    ![](./media/image105.png)

3.  Select **Save**.

    ![](./media/image106.png)

### Task 5: Add condition node 

1.  Select the **+** icon under the topic management node and
    select **Add a condition**.

    ![](./media/image107.png)

2.  Select **DetailsCorrect** for variable.

    ![](./media/image108.png)

3.  Select the **Condition** as **is equal to**

4.  Select the **value** as **Yes**.

    ![](./media/image109.png)

5.  Select **Save**.

    ![](./media/image110.png)

### Task 6: Add question nodes

1.  Select the **+** icon under the left-hand condition node and
    select **Ask a question**. Fill in the below details and click on
    **Save**.

    - Enter a message  - +++Which property do you want to see?+++
    
    - **Identify** - Select **User's entire response**.
    
    - **Save user response as** -
      Enter +++**PropertyName**+++ for **Variable name**

    ![](./media/image111.png)

2.  Select the the **+** icon under the question node and select **Ask a
    question**. Fill in the below details and click on **Save.**

    - **Enter a message** - +++What date and time do you want to see the
      property?+++
    
    - Identify - Select **Date and Time**
    
    - **Save user response as** - Enter +++**DateTime**+++ for **Variable
      name**

    ![](./media/image112.png)

### Task 7: Test the copilot

1.  Select the **Test** button in the top-right of the screen to open
    the testing panel. Select the **three dots** at the top of the
    testing panel in the top-right of the screen. Select **Track between
    topics**.

    ![](./media/image113.png)

2.  When the **Conversation Start** message appears, your copilot starts
    a conversation.

3.  In response, enter a trigger phrase for the topic that you created:

    +++I want to book a real estate showing+++

4.  The copilot responds with the "**What is your name?**" question.

5.  Enter your name.

    ![](./media/image114.png)

6.  Then enter your email when it prompts for the email. After you enter
    the details, an Adaptive Card displays the information that you
    entered, a question asking if the information is correct, and
    options to select **Yes** or **No**. Select **Yes**.

    ![](./media/image115.png)

7.  Enter +++555 Oak Lane, Denver, CO 80203+++ to the **Which property
    to you want to see?** prompt.

8.  Enter **Tomorrow 10:00 AM** to the **What date and time do you want
    to see the property?** prompt.

    ![](./media/image116.png)

## Exercise 6: Connect the copilot to Dynamics 365 Customer Service and configure the Escalate topic

### Task 1: Configure the Escalate topic

1.  Select the **Topics** tab and then select the **System** tab. Select
    the **Escalate** topic.

    ![](./media/image117.png)

2.  Select the message node of the topic and replace the existing
    content with, +++You will be transferred to a live agent shortly+++

    ![](./media/image118.png)

3.  Click on the + symbol to add a node next to the Message node.

4.  Select **Topic management** -\> **Transfer conversation**.

    ![](./media/image119.png)

5.  Give a message +++The customer wants to talk to a live agent+++ in
    the Transfer conversation node.

    ![](./media/image120.png)

6.  **Save** the Topic.

    ![](./media/image121.png)

7.  **Publish** the copilot.

    ![](./media/image122.png)

### Task 2: Connect the copilot to Dynamics 365 Customer Service

1.  Click on the **Overview** option to arrive at the Overview page of
    the copilot.

    ![](./media/image123.png)

2.  From the copilot page top menu, click on **Channels** (If the
    Channels is not visible, click on the +1 to view the **Channels**
    option)

    ![](./media/image124.png)

3.  Select **Dynamics 365 Customer Service** from the Customer
    engagement hub pane.

    ![](./media/image125.png)

4.  On the Dynamics 365 Customer Service page, click on **Connect**.

    ![](./media/image126.png)

5.  Once you get a **successfully connected** message, click on
    **Close**.

    ![](./media/image127.png)

>[!Note] **Note:** Due to very recent changes in the Customer Service admin center, the following two exercises might not work as expected. If you face issues completing it, please pause it for now.

## Exercise 7: Create workstream and channel in Dynamics 365 admin center

### **Task 1: Manage a user in Omnichannel for Customer Service**

1.  Login to +++https://www.office.com+++ using your admin tenant id.

2.  Select **Apps** from the left pane.

    ![](./media/image128.png)

3.  From the list of Apps listed, select **Customer Service admin
    center**.

    ![](./media/image129.png)

4.  In **Dynamics 365 Customer Service admin center**, in the site map,
    select **User management** under **Customer support** group.

5.  On the **User management** page, select **Manage** next
    to **Users**.

    ![](./media/image10.png)

6.  Click the dropdown next to **Enabled Users** and select
    **Omnichannel Users**.

    ![](./media/image11.png)

7.  On the **Omnichannel Users** page, select a user **MOD
    Administrator** in the list.

    ![](./media/image12.png)

8.  On the **MOD Administrator** page, select the **Omnichannel** tab.

    ![](./media/image13.png)

9.  Specify the following in the user page.

    | **Setting**      | **Value** |
    |------------------|-----------|
    | Capacity         | 100       |
    | Default Presence | available |

    ![](./media/image14.png)

10.  Select **Save and close**.

    ![](./media/image15.png)
    
### Task 1: Configure workstream 

1.  From the admin center page, select **Workstreams** from the left
    pane and then select the **+ New workstream** option.

    ![](./media/image130.png)

2.  Fill in the below details, scroll down and click on **Create**.

    - Name - +++**Real Estate Workstream**+++
    
    - Owner – **MOD Administrator** (Selected by default)
    
    - Type – **Messaging**
    
    - Channel – **Chat**

    ![](./media/image131.png)

    ![](./media/image132.png)

3.  Once the workstream is created, click on **Set up chat** to set up
    the chat channel.

    ![](./media/image133.png)

4.  In the **Live chat setup – Channel details** screen, fill in the
    below details and click on **Next**.

    - Name - +++**Real Estate Chat Channel**+++
    
    - Language – **United States**

    ![](./media/image134.png)

5.  In the Live chat setup – Chat widget screen, provide the name as
    +++**Real Estate Booking Assistant**+++, accept the other defaults
    and click on **Next**.

    ![](./media/image135.png)

6.  In the **Live chat setup – Behaviors** screen, accept the defaults
    and click on **Next**.

    ![](./media/image136.png)

7. In the **Live chat setup – User features** screen, toggle **File
    attachment** and **Voice and video calls** options to **off** and
    click on **Next**.

    ![](./media/image137.png)

8. In the **Live chat setup – Review and finish** screen, select
    **Create channel**.

    ![](./media/image138.png)

9. **Copy** the widget that appears in the **Live chat setup –
    Success** screen and **save** it in a notepad to add it to a webpage
    in the upcoming exercises. Then, click on **Done** to complete the
    configuration.

    ![](./media/image139.png)

### Task 3: Add the copilot to the workstream

1.  Back in the **Real Estate Workstream** page, scroll down and click
    on **+ Add bot** in the Bot section.

    ![](./media/image140.png)

2.  From the list of copilots on the Add bot screen, select the **Real
    Estate Booking Service** copilot and click on **Connect**.

    ![](./media/image141.png)

3.  Ensure that the bot is added to the workstream as in the screenshot
    below.

    ![](./media/image142.png)

4.  From the left pane, select **Bots**.

    ![](./media/image143.png)

5.  Ensure that the Real Estate Booking Service copilot is connected.

    ![](./media/image144.png)

## Exercise 8: Create a webpage and test the escalation to agent

1.  Login to +++https://make.powerpages.microsoft.com/+++ using your
    tenant admin credentials.

    ![](./media/image145.png)

2.  Ensure that you are in CustomerService Trial environment.

3.  Click on Skip in the **Tell us about yourself** page.

    ![](./media/image146.png)

4.  Scroll down in the next page and click on Start with a template
    option to start creating the site with a template.

    ![](./media/image147.png)

5.  Select a template and click on **Choose this template**.

    ![](./media/image148.png)

6.  In the Give your site a name textbox, enter the name as +++**Contoso
    Real Estates**+++, accept the other defaults and click on **Done**.

    ![](./media/image149.png)

7.  Once the site is created, click on **Edit site header** in the
    **Company name** title.

    ![](./media/image150.png)

8.  In the **Edit site header** pane, provide the **Site title** as
    **Contoso Real Estates**.

    ![](./media/image151.png)

9.  Click on Edit code in the top right corner of the page.

    ![](./media/image152.png)

10. Click on **Open Visual Studio Code**.

    ![](./media/image153.png)

11. Click **Allow**.

    ![](./media/image154.png)

12. The Home page of the web page opens up in the Visual Studio Code.

    ![](./media/image155.png)

13. Scroll to the end of the file. Add the script copied while creating
    the workstream, after eh last line of this file.

    ![](./media/image156.png)

14. Save the file, close the Visual Studio Code tab and return to the
    Power pages. Click on **Sync**.

    ![](./media/image157.png)

15. Once the Sync is completed, select **Preview** -\> **Desktop.**

    ![](./media/image158.png)

16. Your web page opens in a new tab. Find the **Real Estate copilot**
    embedded to the page at the bottom right of the web page. **Click**
    on it.

    ![](./media/image159.png)

17. Enter +++Talk to agent+++.

    ![](./media/image160.png)

18. On the Customer Service workspace page, you will get a **chat
    request**. Accept it.

    ![](./media/image161.png)

19. Once accepted, the chat screen opens up with the message that we had
    given in the Escalate topic. We can also add any other information
    provided by the user here to the live agent.

    ![](./media/image162.png)

20. Simulate the chat between the live agent and the customer if you
    wish to see how it works and then ends.

    ![](./media/image163.png)

    ![](./media/image164.png)

**Summary**

In this lab, we have learnt to

- Build a copilot from the Copilot Studio and create topics in it.

- Test the copilot from the Copilot Studio and publish it to the demo
  web site.

- Publish the copilot to Dynamics 365 workspace and integrate the it in
  a web page.

- Configure and test the escalation to a live agent.

## Exercise 1: Use entities to improve the copilot

Microsoft Copilot Studio uses entities to understand user intent. There
are many prebuilt entities included for commonly used information. You
can create custom entities for your specific purpose.

### Task 1: View prebuilt entities

1.  Select **Settings** in the top-right of the screen.

    ![](./media/image1.png)

2.  Select the **Entities** tab. You can see a list of pre-built
    entities.

    ![](./media/image2.png)

### Task 2: Create the property type entity

1.  Select **+ Add an entity** and select **+ New entity**.

    ![](./media/image3.png)

2.  Select the **Closed list** tile.

    ![](./media/image4.png)

3.  Enter the below details

    -    Name - +++**Property Type**+++
    
    **Enter item** under List items
    -    +++**Apartment**+++ - Select **Add**

    ![](./media/image5.png)

4.  Enter +++**Condominium**+++ in the **Enter item** field and
    select **Add**.

5.  Enter +++**Duplex**+++ in the **Enter item** field and
    select **Add**.

    ![](./media/image6.png)

6.  Select **+ Synonyms** for **Apartment**, enter +++**Flat**+++, then
    select the **+** icon and select **Done**.

    ![](./media/image7.png)

7.  Select **+ Synonyms** for **House**, enter +++**Single-family
    home**+++, then select the **+** icon and select **Done**.

8.  Select **+ Synonyms** for **Condominium**,
    enter +++**Townhouse**+++, then select the **+** icon and
    select **Done**.

9.  Select **Save**.

    ![](./media/image8.png)

10. Select **Close**.

    ![](./media/image9.png)

### Task 3: Create number of bedrooms entity

1.  Select **+ Add an entity** and select **+ New entity**.

    ![](./media/image10.png)

2.  Select the **Regular expression (Regex)** tile.

    ![](./media/image11.png)

3.  Enter the below details and click on **Save**.

    - Name  - +++**Number of Bedrooms**+++ 
    
    - Pattern  - +++**\[1-5\]**+++ 

    ![](./media/image12.png)

4.  Select **Close**.

    ![](./media/image13.png)

5.  Close the **Settings** pane.

    ![](./media/image14.png)

### Task 4: Use entities

1.  Select the **Topics** tab. Select the **Book a Real Estate
    Showing** topic.

    ![](./media/image15.png)

2.  Select the **+** icon above the property question node and
    select **Ask a question**.

    ![](./media/image16.png)

3.  Fill in the below details.

    - **Enter a message** - +++What type of property do you want to see?+++
    
    - **Identify** – Select **Property Type**
    
    - Select **Select options for user** and check the **Display** option
      for all list values.

    ![](./media/image17.png)

4.  Select the variable in **Save user response as** and enter
    +++**PropertyType**+++ for **Variable name**

    ![](./media/image18.png)

5.  Select the the **+** icon below the new question node and
    select **Ask a question**.

6.  Enter the below details and click on **Save**.

    - **Enter a message** - +++How many bedrooms do you need?+++
    
    - **Identify -** Select **Number of Bedrooms**
    
    - **Save user response as** -
      Enter +++NumberofBedrooms+++ for **Variable name**

    ![](./media/image19.png)

## Exercise 2: Create Copilot actions

Microsoft Copilot Studio can access data in Microsoft Dataverse using
Power Automate cloud flows

### Task 1: Create Power Automate flow to retrieve a property

1.  Select the **Actions** tab from the top menu. Select **+ Add an
    action**.

    ![](./media/image20.png)

2.  Scroll down and select **Create a new flow**.

    ![](./media/image21.png)

3.  Sign in to Power Automate if prompted.

4.  Select **Run a flow from Copilot** in the top-left of the screen and
    enter +++**Get Property**+++ as the flow name.

    ![](./media/image22.png)

5.  Select the trigger step **Run a flow from Copilot** and select **+
    Add an input**.

    ![](./media/image23.png)

6.  Select **Text**.

    ![](./media/image24.png)

7.  Enter the below details

    - **Input** – +++Bedrooms+++
    
    - **Please enter your input** - +++Number of Bedrooms+++

    ![](./media/image25.png)

8.  Select the **+** icon between the two steps in the flow and
    select **Add an action**.

    ![](./media/image26.png)

9.  Enter +++**Dataverse**+++ in the **Search** field and select **See
    more** for the Dataverse connector.

    ![](./media/image27.png)

10. Select the **List rows** action.

    ![](./media/image28.png)

11. If prompted for authentication, select **OAuth** and select **Sign
    in**. Sign in using your tenant id if prompted.

    ![](./media/image29.png)

12. Select **Real Estate Properties** for table name.

13. Select **Show all**.

14. Enter +++contoso_bedrooms eq+++ in the **Filter Rows** field.

15. Use **Dynamic content** to select the **Bedrooms** parameter and
    select **Add**.

    ![](./media/image30.png)

16. Select the **Respond to Copilot** action and select **+ Add an
    output**.

    ![](./media/image31.png)

17. Select **Text**.

18. Enter the below details

    - **Enter a name** - +++PropertyId+++
    
    - **Enter a value to respond with** - select **Insert Expression** and
      enter the following expression:
      +++first(outputs('List_rows')?\['body/value'\])\['contoso_realestatepropertyid'\]+++

    ![](./media/image32.png)

19. Select **Add**.

    ![](./media/image33.png)

20. Select **+ Add an output**.

21. Select **Text**.

    - **Enter a name** - +++PropertyName+++ 
    
    - **Enter a value to respond with** - select **Insert Expression** and
      enter the following expression:
      +++first(outputs('List_rows')?\['body/value'\])\['contoso_propertyname'\]+++

    ![](./media/image34.png)

22. Select **Settings**. Ensure that **Asynchronous Response** is set
    to **Off**.

    ![](./media/image35.png)

23. Select **Save draft**.

    ![](./media/image36.png)

24. Once save, select **Publish**.

    ![](./media/image37.png)

25. Close the Power Automate tab.

### Task 2: Add a Copilot action for retrieving a property

1.  Back in the Copilot Studio page, select **Refresh**.

    ![](./media/image38.png)

2.  Select the **Get Property** flow.

    ![](./media/image39.png)

3.  Select **Next** in the **Choose an action** screen.

    ![](./media/image40.png)

4.  Select **Next** in the **Review inputs and outputs** screen.

    ![](./media/image41.png)

5.  Select **Finish** in the **Review and finish** screen.

    ![](./media/image42.png)

6.  Select the **Topics** tab. And select the **Book a Real Estate
    Showing** topic.

    ![](./media/image43.png)

7.  Select the **+** icon below the **How many bedrooms do you need
    question?** node and select **Call an action**. Select the **Get
    Property** flow.

    ![](./media/image44.png)

8.  Select the **NumberofBedrooms** variable for the **Bedrooms** input
    parameter.

    ![](./media/image45.png)

9.  Select the **three dots** in the **Which property do you want to
    see?** question node and select **Delete**.

    ![](./media/image46.png)

10. Select the the **+** icon under the action node and select **Send a
    message**.

11. Fill in the below details

    - **Enter a message** - enter +++Property+++
    
    - Select the **Insert variable** icon and select
      the **PropertyName** variable.

    ![](./media/image47.png)

12. Select **Save**.

    ![](./media/image48.png)

13. Once saved, select **Publish** and select **Publish**.

    ![](./media/image49.png)

14. Click on Publish in the Publish confirmation dialog.

    ![](./media/image50.png)

### Task 3: Create Power Automate flow to make a booking

1.  Select the **Actions** tab and select **+ Add an action**.

    ![](./media/image51.png)

2.  Scroll down and select **Create a new flow**.

    ![](./media/image52.png)

3.  Select **Run a flow from Copilot** in the top-left of the screen and
    enter Create +++**Booking Request**+++ as the flow name.

    ![](./media/image53.png)

4.  Select the trigger step **Run a flow from Copilot** and select **+
    Add an input -\> Text**.

    ![](./media/image54.png)

    ![](./media/image55.png)

5.  Enter the below details

    - Input - +++**PropertyId**+++
    
    - Please enter your input **-** +++**Property**+++

6.  Select **+ Add an input -\> Text**

    - Input - +++**ViewerName**+++
    
    - Please enter your input **-** +++**Viewer Name**+++

7.  Select **+ Add an input -\>** **Text**.

    - Input - +++**ViewerEmail**+++
    
    - Please enter your input **-** +++**Viewer Email**+++

    ![](./media/image56.png)

8.  Select the **+** icon between the two steps in the flow and
    select **Add an action**.

    ![](./media/image57.png)

9.  Enter +++**Dataverse**+++ in the **Search** field and select **See
    more** for the Dataverse connector.

    ![](./media/image58.png)

10. Select the **Add a new row** action.

    ![](./media/image59.png)

11. Select **Booking Requests** for table name.

12. Enter +++**Copilot booking**+++ in the **Booking Name** field.

13. Select **Show all**.

    ![](./media/image60.png)

14. Enter +++contoso_bookingrequests()+++ in the **Property (Real Estate
    Properties)** field, move the cursor within the brackets, and
    use **Dynamic content**.

    ![](./media/image61.png)

15. Select the **PropertyId** parameter.

    ![](./media/image62.png)

16. Use **Dynamic content** to select the **ViewerName** parameter for
    the **Viewer Name** field.

    ![](./media/image63.png)

17. Use **Dynamic content** to select the **ViewerEmail** parameter for
    the **Viewer Email** field.

    ![](./media/image64.png)

18. The parameters will now look similar to those in the screenshot
    below.

    ![](./media/image65.png)

19. Select the **Respond to Copilot** action. Select **Settings** and
    ensure that **Asynchronous Response** is set to **Off**.

    ![](./media/image66.png)

20. Select **Save draft**.

    ![](./media/image67.png)

21. Once saved, select **Publish**.

    ![](./media/image68.png)

22. Close the Power Automate tab.

### Task 4: Add a Copilot action for creating a booking request

1.  Back in the Copilot Studio page, select **Refresh**.

    ![](./media/image69.png)

2.  Select the **Create Booking Request** flow.

    ![](./media/image70.png)

3.  Select **Next** in the Choose an option screen.

    ![](./media/image71.png)

4.  Select **Next** in the Review inputs and outputs .

    ![](./media/image72.png)

5.  Select **Finish** in the **Review and finish** screen.

    ![](./media/image73.png)

6.  Select the **Topics** tab and select the **Book a Real Estate
    Showing** topic.

    ![](./media/image74.png)

7.  Select the the **+** icon below the **What date and time do you want
    to see the property?** node and select **Call an action**.

8.  Select the **Booking Request** flow.

    ![](./media/image75.png)

9.  Select the **PropertyId** variable for the **PropertyId** input
    parameter.

    Select the **Name** variable for the **ViewerName** input parameter.

    Select the **EmailAddress** variable for the **ViewerEmail** input
parameter.

    ![](./media/image76.png)

10. Select the the **+** icon below the action node. Select **Topic
    management**, then select **Go to another topic** and select **End
    of conversation**.

    ![](./media/image77.png)

11. Select **Save**.

    ![](./media/image78.png)

12. Once saved, select **Publish** and select **Publish** again in the
    confirmation dialog.

    ![](./media/image79.png)

    ![](./media/image80.png)

## Exercise 3: Test the copilot 

### Task 1: Test the copilot and make a booking request

1.  Select the **Test** button in the top-right of the screen to open
    the testing panel. Select the **three dots** at the top of the
    testing panel in the top-right of the screen. Select **Track between
    topics**.

    ![](./media/image81.png)

2.  When the **Conversation Start** message appears, your copilot starts
    a conversation.

3.  When the **Conversation Start** message appears, your copilot starts
    a conversation.

4.  In response, enter a trigger phrase for the topic that you created:

+++I want to book a real estate showing+++

5.  The copilot responds with the "**What is your name?**" question.

6.  Enter your name.

    ![](./media/image82.png)

7.  Then enter your email when it prompts for the email. After you enter
    the details, an Adaptive Card displays the information that you
    entered, a question asking if the information is correct, and
    options to select **Yes** or **No**. Select **Yes**.

    ![](./media/image83.png)

8.  Select **House** for the type of property prompt.

9.  Enter +++**2**+++ for the number of bedrooms prompts.

    ![](./media/image84.png)

10. Enter Tomorrow 2:00 PM to the **What date and time do you want to
    see the property?** prompt.

11. Select **Yes** to the **Did that answer your question?** prompt.

12. Select any rating.

13. Select **No** to the **Can I help with anything else?** prompt.

    ![](./media/image85.png)

### Task 2: Verify booking request

1.  Navigate to the Power Apps portal at
    +++**https://make.powerapps.com**+++.

2.  In the left navigation pane, select **Tables** and
    select **Custom**.

3.  Select the **Booking Request** table.

    ![](./media/image86.png)

4.  Under **Booking Request columns and data** you should see that a
    Copilot booking request is now created.

    ![](./media/image87.png)

## Exercise 4: Set up Generative AI

In this exercise, you learn how to use the Generative answers feature to
improve your copilot's responses.

### Task 1: Enable Generative AI

1.  Login to the Copilot Studio using your tenant credentials at
    +++https://copilotstudio.microsoft.com+++ if not logged in
    already.

2.  Select the Copilot **Real Estate Booking Service**.

    ![](./media/image88.png)

3.  Select **Settings** in the top-right of the screen.

    ![](./media/image89.png)

4.  Select the **Generative AI** tab.
   
    -    Select **Generative** under **How should your copilot decide how to respond**.
    -    Select **Medium** for **Copilot content moderation**.
    -    Select **Save**.
    -    
    ![](./media/image90.png)

5.  **Close** the Settings pane.

    ![](./media/image91.png)

### Task 2: Enable knowledge

1.  Select your copilot in the Copilot pane on the left-hand side of the
    screen to return to the **Overview** tab.

2.  Verify that general knowledge is enabled in the Knowledge section.

    ![](./media/image92.png)

### Task 3: Add knowledge from a website

1.  Select **+ Add knowledge** under the **Knowledge** section in the
    Overview page of the copilot.

    ![](./media/image93.png)

2.  Select the **Public websites** tile.

    ![](./media/image94.png)

3.  Enter the public website
    link +++https://create.microsoft.com/templates/real-estate+++.
    Select **Add**.

    ![](./media/image95.png)

4.  Give the name +++Real Estate Website+++ in the Name field and then
    select **Add**.

    ![](./media/image96.png)

### Task 4: Add knowledge from Dataverse

1.  Select the **Knowledge** tab. Select **+ Add knowledge**.

    ![](./media/image97.png)

2.  Select **Dataverse**.

    ![](./media/image98.png)

3.  Select the **Real Estate Property** table and select **Next**.

    ![](./media/image99.png)

4.  Preview the data in the next screen and then select **Next**.

    ![](./media/image100.png)

5.  Review the details and click on **Add** in the Review and finish
    screen.

    ![](./media/image101.png)

### Task 5: Add knowledge from files

1.  From the **Knowledge** tab, select **+ Add knowledge**.

    ![](./media/image102.png)

2.  Select **Files**.

    ![](./media/image103.png)

3.  Select Click to browse and browse to locate the file
    **SummitRealtyCaseStudy.docx** at **C:\LabFiles** and select it.

    ![](./media/image104.png)

4.  Select **Add**.

    ![](./media/image105.png)

### Task 6: Use generative answers in System fallback topic

1.  Select the **Topics** tab and select **System**. Select
    the **Fallback** topic.

    ![](./media/image106.png)

2.  Select the **three dots** in the message node and select **Delete**.

    ![](./media/image107.png)

3.  Select the **+** icon under the Condition node, select **Advanced**,
    and select **Generative answers**.

    ![](./media/image108.png)

4.  Select the **Input** field, select **System** in the **Select a
    variable** pane. Select **Activity.Text** from it.

    ![](./media/image109.png)

5.  Select **Edit** under **Data sources**.

    ![](./media/image110.png)

6.  Select **Search only selected sources**.

    ![](./media/image111.png)

7.  Select the **SummitRealtyCaseStudy** document. Deselect **Allow the
    AI to use its own general knowledge**.
    Select **Medium** for **Content moderation**.

    ![](./media/image112.png)

8.  Select **Save**.

    ![](./media/image113.png)

### Task 7: Configure Security

1.  Select your copilot in the Copilot pane on the left-hand side of the
    screen to return to the **Overview** tab.

2.  From the copilot page top menu, click on **Channels** (If the
    Channels is not visible, click on the +1 to view the **Channels**
    option)

    ![](./media/image114.png)

3.  Select **Dynamics 365 Customer Service** from the Customer
    engagement hub pane.

    ![](./media/image115.png)

4.  On the Dynamics 365 Customer Service page, click on **Disconnect**.

    ![](./media/image116.png)

5.  Once done, **close** the Dynamics 365 Customer Service pane.

    ![](./media/image117.png)

6.  Select **Settings** in the top-right of the screen.

    ![](./media/image118.png)

7.  Select the **Security** tab and then select
    the **Authentication** tile.

    ![](./media/image119.png)

8.  Select Authenticate with Microsoft **(Entra ID authentication in
    Teams and Power App)**.

9.  Select **Save**.

    ![](./media/image120.png)

10. Select **Save**.

    ![](./media/image121.png)

11. Select **Close**.

    ![](./media/image122.png)

12. Select your copilot in the Copilot pane on the left-hand side of the
    screen to return to the **Overview** tab.

13. Select **Publish** and select **Publish**.

    ![](./media/image123.png)

### Task 8: Test the copilot's knowledge

1.  Select the **Test** button in the top-right of the screen to open
    the testing panel.

    ![](./media/image124.png
    )

3.  Select the **three dots** at the top of the testing panel in the
    top-right of the screen.

4.  Select **Track between topics**.

5.  Select the **Start a new conversation** icon at the top of the
    testing panel.

6.  Explore the copilot and see how it uses the different knowledge
    sources.

**Summary:**

In this lab, we have learnt to

- Use entities and slot filling

- Implement Flow actions

- Add knowledge to the copilot

- Enable Generative AI
