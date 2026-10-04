---
#icon: material/folder-open-outline
icon: material/medal
---

# Mission 3: Configure Fulfillment Action and create an order using **Voice Flow**.

**<details><summary>What is Fulfillment Action? <span style="color: orange;"></span></summary>**

Fulfillment Action is a task that an AI agent performs by understanding user intents and completes by connecting to external systems over an API.


## </details>

## Mission overview


In this mission, you will use the Voice flow to execute the API call that creates the order and completes the AI Agent Fulfillment.

![Profiles](../graphics/Lab1_AI_Agent/Fulfilment.png)

---

## Build


### Task 1. Configure Action in the AI Studio

1. Go to **Webex AI Agent** Studio Portal.

2. Select your AI agent with name **<copy><w class="attendee"></w>\_2000_AutoAI_Lab</copy>** that you created earlier and go to **Actions**. You will see one Action is already created by default for the Agent Handoff. We will now create a few more actions.
   ![Profiles](../graphics/Lab1_AI_Agent/2.17.gif)

3. Click to create <b>New Action</b>. From the drop-down option, select **Fulfillment**.
   ![Profiles](../graphics/Lab1_AI_Agent/2.18.png)

4. Configure it with name **_<copy>Create_New_Order</copy>_** and the Action description **_<copy>Collect order details, delivery address, total and respond with the ID number once the order is completed. The request will contain the order details. From the order details let the customer know the order ID.</copy>_**.
   ![Profiles](../graphics/Lab1_AI_Agent/2.18a.gif)

5. Scroll down and click to create **New input entity**. Fill up the table with the following and then click on **Add**. <br>
   > Entity Name: **_<copy>address</copy>_** <br>
   > Entity Type: <b>string</b> <br>
   > Description: **_<copy>Collect the customer's delivery address</copy>_**<br>
   > Example: **_<copy>548 Catalina Drive, Cary, NC 27515</copy>_** <br>
   > Required: <b>Yes</b>
   ![Profiles](../graphics/Lab1_AI_Agent/2.19.gif)

6. By following the same pattern, create an entity to collect the customer's phone number.<br>
   > Entity Name: **_<copy>phoneNumber</copy>_**<br>
   > Entity Type: <b>string</b> <br>
   > Description: **_<copy>Collect customer's phone number. Before the customer completes the order, ask if they would like to receive confirmation over the SMS. If so, collect the phone number.</copy>_**<br>
   > Example: **_<copy>3477579861</copy>_**<br>
   > Required: <b>Yes</b>

7. By following the same pattern, create an entity to collect the customer's order details.<br>
   > Entity Name: **_<copy>orderDetails</copy>_**<br>
   > Entity Type: <b>string</b> <br>
   > Description: **_<copy>Collect the flowers and bouquets information that customer orders. Make sure to do correct math. If one rose is 20 dollars and the customer would like to buy 9 roses then the price should be 180 dollars. Don't use double quotes (") in the generated responses.</copy>_**<br>
   > Example: **_<copy>Romantic Roses standard bouquet and one more bouquet with 9 roses</copy>_**<br>
   > Required: <b>Yes</b>

8. By following the same pattern, create an entity to store the total price information of the order.<br>
   > Entity Name: **_<copy>orderTotal</copy>_**<br>
   > Entity Type: <b>string</b> <br>
   > Description: **_<copy>After the customer informs if they need delivery or not, and confirm that they would like to proceed with completing the order, collect the Total information and assign it to this slot. Always use the number for the total. For example use 500 $ but not five hundred dollars.</copy>_**<br>
   > Example: **_<copy>150 dollars, 70 dollars</copy>_**<br>
   > Required: <b>Yes</b>

9. By following the same pattern, create an entity to store the order status information.<br>
   > Entity Name: **_<copy>status</copy>_**<br>
   > Entity Type: <b>string</b> <br>
   > Description: **_<copy>Always create it as "new"</copy>_**<br>
   > Example: **_<copy>new</copy>_**<br>
   > Required: <b>Yes</b>

10. At this point you should see 5 created entities. Please double-check that your configuration matches the screenshot below.
    ![Profiles](../graphics/Lab1_AI_Agent/2.61.png)


11. Scroll down and for the **Fulfillment** option select **Manage in the source flow (voice only)**. Click **Save**.
   ![Profiles](../graphics/Lab1_AI_Agent/19.2.png)

12. **Publish** your AI Agent.
   ![Profiles](../graphics/Lab1_AI_Agent/19.33awww.png)


### Task 2. Test Fulfillment.



1. Place a test call, order flowers, and specify a number for SMS confirmation. Your order should be completed, and you should receive the SMS.

    ![Profiles](../graphics/Lab1_AI_Agent/19.33a.png)

2. <span style="color: red;">**[Read Only]**</span> In the voice flow, the fulfillment branch was already preconfigured for this lab. You can review the configuration to understand it by tracing the call in the flow designer. In the flow designer, we use an **HTTP Request** node to send an HTTP request to a third-party application to create an order object. Then we send these results to the caller over SMS, and we send the order details back to the AI Agent in the **State Event**.

    ![Profiles](../graphics/Lab1_AI_Agent/19.33b.png)
<p style="text-align:center"><strong>Congratulations, you have officially completed this mission! 🎉🎉 </strong></p>
