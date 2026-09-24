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
   ![Profiles](../graphics/Lab1_AI_Agent/19.33.gif)

### Task 3. Configure fulfillment logic in the Voice flow.

1. In **Collaboration Control Hub**, go to Flows and open your flow with name **<copy>AutonomousAI_Flow_2000_<w class="attendee"></w></copy>**. Click on **Edit**.
   ![Profiles](../graphics/Lab1_AI_Agent/19.3.gif)

2. Remove the **DisconnectContact** node.
   ![Profiles](../graphics/Lab1_AI_Agent/19.4.gif)

3. Create a flow string variable with name **<copy>event_name</copy>** and empty default value.
   ![Profiles](../graphics/Lab1_AI_Agent/19.5.gif)

4. Create a flow string variable with name **<copy>order_request_details</copy>** and empty default value.
   ![Profiles](../graphics/Lab1_AI_Agent/19.6.gif)

5. Add a **SetVariable** node.
   ![Profiles](../graphics/Lab1_AI_Agent/19.7.gif)

6. Click on the **SetVariable** that you just created and configure your **event_name** variable to be assigned with the **VirtualAgentV2....StateEventName** variable. </br>
   **Note:** *This event name will be the same as your Action name from the AI Agent Studio that is used for the fulfillment.*
   ![Profiles](../graphics/Lab1_AI_Agent/19.8.gif)

7. Add one more **SetVariable** node and connect them in series.
   ![Profiles](../graphics/Lab1_AI_Agent/19.9.gif)

8. In the **SetVariable** node click on **Add new** and select Variable as **order_request_details** string variable. To assign the Virtual Agent metadata details to this variable you can either type metadata in the {% raw %}{{}}{% endraw %} and you will see it, or you can click on the **VirtualAgentV2** node, on the right side scroll down until you see the Activity output variable. Copy the name of the variable related to MetaData. Go back to your SetVariable node and configure **order_request_details** with the value of the Metadata that you copied inside of the {% raw %}{{}}{% endraw %}. See the gif below.
   ![Profiles](../graphics/Lab1_AI_Agent/19.10.gif)

9. Add a **Case** node and connect the **SetVariable** node to the **Case** node.
   ![Profiles](../graphics/Lab1_AI_Agent/19.11.gif)

10. Add **Disconnect Contact** and assign the **Default** output of the **Case** node to the **Disconnect Contact**.
   ![Profiles](../graphics/Lab1_AI_Agent/19.12.gif)

11. Click on the **Case** node. Select **event_name** as the Case Variable. Remove the second Link Description. Keep only one Link Description, as for now you have only one action for fulfillment. In the Link Description provide the name of your action: **<copy>Create_New_Order</copy>**.
   **Note:** *If you add more actions later, the Case node is used as the distribution logic for different fulfillment requests.*
   ![Profiles](../graphics/Lab1_AI_Agent/19.13.gif)

12. Add an **HTTP Request** node and connect the **Case** output link to the **HTTP Request** node.
   ![Profiles](../graphics/Lab1_AI_Agent/19.14.gif)

13. Configure the **HTTP Request** with the following:

    - Use authenticated endpoint: **Off**
    - Request URL: **<copy>https://67e9aa0bbdcaa2b7f5b9ed62.mockapi.io/customerOrder</copy>**
    - Method: **POST**
    - Content type: **Application/JSON**
    - Request body: **<copy>{% raw %}{{order_request_details}}{% endraw %}</copy>**
       ![Profiles](../graphics/Lab1_AI_Agent/19.15.gif)

14. Connect the **HTTP Request** node to the **VirtualAgentV2** node.
   ![Profiles](../graphics/Lab1_AI_Agent/19.16.gif)

15. Click on the **VirtualAgentV2** node, open **State Event** and configure the **Event Name** as **<copy>{% raw %}{{event_name}}{% endraw %}</copy>**. In this case, when the interaction returns to the AI agent it stays in the same session and the AI agent continues the conversation accordingly.
   ![Profiles](../graphics/Lab1_AI_Agent/19.17.gif)

16. Next you need to bring the API call results back to your AI agent. For this, click on the **HTTP Request** node, scroll down on the right side and copy the name of the HTTPRequest...ResponseBody. Then go to the **VirtualAgentV2** node, open the **State Events**, and insert the HTTP body response to the **Event Data** inside of the {% raw %}{{}}{% endraw %}. See the steps on the gif below.
   ![Profiles](../graphics/Lab1_AI_Agent/19.17_.gif)

17. Enable decryption in the flow so you can monitor your further test call details.
   ![Profiles](../graphics/Lab1_AI_Agent/19.19.gif)

18. **Validate** and **Publish** the flow with the **Latest** tag.
   ![Profiles](../graphics/Lab1_AI_Agent/19.18.gif)

19. Place a test call to your test number. Ask to order flowers, and provide the requested information. You should hear that the order was completed successfully. If you have an issue, you can troubleshoot using the flow debugger. First trace the call in the voice flow to make sure the HTTP request was successful. Click on the HTTP Request node, decrypt the results to make sure you got a 201 status result.
   ![Profiles](../graphics/Lab1_AI_Agent/19.20.gif)



### Task 4. Configure SMS Confirmation.

1. Create a new JSON variable with the following:

    - Name: **<copy>Order_SMS</copy>**
    - Variable Type: **JSON**
    - Default Value: **<copy>{}</copy>**
       ![Profiles](../graphics/Lab1_AI_Agent/19.26.gif)

2. Delete the link between the **HTTP Request** and **VirtualAgentV2** nodes.
   ![Profiles](../graphics/Lab1_AI_Agent/19.33.gif)

3. Bring the **SetVariable** node and connect the **HttpRequest** node to this **SetVariable** node.
   ![Profiles](../graphics/Lab1_AI_Agent/19.33ab.gif)

4. In the **SetVariable** node, configure the **Order_SMS** variable with the outbound body variable from the **HTTP Request** node. Please check the gif below.
   ![Profiles](../graphics/Lab1_AI_Agent/19.33abck.gif)

5. Bring the **Parse** node and connect the **SetVariable** node to the **Parse** node.
   ![Profiles](../graphics/Lab1_AI_Agent/19.33abc.gif)

6. Create a new String variable with the following:

    - Name: **<copy>PhoneNumber_SMS</copy>**
    - Variable Type: **String**
       ![Profiles](../graphics/Lab1_AI_Agent/19.33abcd.gif)

7. Click on the **Parse** node and configure it with the following:

    - Input variable: **<copy>Order_SMS</copy>**
    - Variable Type: **JSON**
    - Output variable: **<copy>PhoneNumber_SMS</copy>**
    - Path expression: **<copy>$.phoneNumber</copy>**
       ![Profiles](../graphics/Lab1_AI_Agent/19.33abce.gif)

8. Bring the **Send SMS** node and connect the **Parse** node to the **Send SMS** node.
   ![Profiles](../graphics/Lab1_AI_Agent/19.33abcf.gif)

9. Click on the **Send SMS** node and configure it with the following:

    - To number: **<copy>{% raw %}{{PhoneNumber_SMS}}{% endraw %}</copy>**
    - Entry point: **CCBU_SMS**
    - Message type: **<copy>Text</copy>**
    - Message content: **<copy>{% raw %}{{Order_SMS}}{% endraw %}</copy>**
       ![Profiles](../graphics/Lab1_AI_Agent/19.33abcg.gif)

10. Connect the **Send SMS** node to the **VirtualAgentV2** node.
   ![Profiles](../graphics/Lab1_AI_Agent/19.33abch.gif)

11. **Validate** and **Publish** the flow.
   ![Profiles](../graphics/Lab1_AI_Agent/19.33abcj.gif)

12. Place a test call, create an order with a number for SMS confirmation, and you should receive the SMS.
   ![Profiles](../graphics/Lab1_AI_Agent/19.33a.png)



<p style="text-align:center"><strong>Congratulations, you have officially completed the Autonomous AI Agent lab! 🎉🎉 </strong></p>
