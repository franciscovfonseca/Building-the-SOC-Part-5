<br>

<h1 align="center">Stage II - Building the SOC - Part 5</h1>

<br>

<h2 align="center">Configure Microsoft Sentinel</h2>

<p align="center">
<img width="800" src="https://github.com/user-attachments/assets/39d59344-9d47-4be6-aba0-7ba2ead7efba" alt="Banner"/>
<br />
<br />

In this Lab we're going to create 4 diffferent World Maps

We'll map out where different people around the World are doind Malicious things to our Environment since its been online.

<br>


So basically we're going to **Build 4 Attack Maps for the Following Use Cases**:


1. Failed Authentication against **Windows WMs** (RDP / SMB / General Authentication Failures)

2. Failed Authentication against **Linux VM** (SSH)

3. Failed Authentication to the **Microsoft SQL Server** (inside our Windows VM)

4. Malicious Inbound Flows for the **Network Security Groups**


<br>

<br>

<details close> 
<summary> <h2>1️⃣ World Attack Maps Construction</h2> </summary>
<br>


Go to **Microsoft Sentinel** ➜ select our Log Analytics Workspace ```LAW-Cyber-Lab``` that is associated with this Sentinel Instance.

Click on the **Workbooks** blade ➜ and then ➕ **Add Workbook**

<br>

![azure portal](https://github.com/user-attachments/assets/ed64370f-008f-4711-8e7d-25401d8a29a8)

<br>

<details close> 
  
**<summary> 📝 Step-by-step Guide on How to Create the Sentinel Maps Inside the Workbooks?</summary>**

<br>

We'll first create the **Workbook** & the **Map** for the ***Linux SSH Authentication Failures***

After clicking on ➕ **Add Workbook** ➜ you can see there's a Default Workbook that Sentinel made.

Click ✏️ **Edit**

<br>

![azure portal](https://github.com/user-attachments/assets/ed64370f-008f-4711-8e7d-25401d8a29a8)

<br>

There's 2 Elements in the default workbook ➜ so we'll 🗑️ **Remove** them both

<br>

![azure portal](https://github.com/user-attachments/assets/ed64370f-008f-4711-8e7d-25401d8a29a8)

<br>

![azure portal](https://github.com/user-attachments/assets/ed64370f-008f-4711-8e7d-25401d8a29a8)

<br>

Then we're going to click on ➕ **Add** ➜ and we're going to 𝄜 **Add query** based element

<br>

![azure portal](https://github.com/user-attachments/assets/ed64370f-008f-4711-8e7d-25401d8a29a8)

<br>

We'll then click the **</> Advanced Editor blade**

<br>

![azure portal](https://github.com/user-attachments/assets/ed64370f-008f-4711-8e7d-25401d8a29a8)

<br>

Now go to [this GitHub link](https://github.com/joshmadakor1/Cyber-Course-v2/blob/main/Sentinel-Maps(JSON)/linux-ssh-auth-fail.json) to get the **JSON** for the **Linux SSH Failed Authentication Map**.

Copy the **JSON** text.

<br>

![azure portal](https://github.com/user-attachments/assets/ed64370f-008f-4711-8e7d-25401d8a29a8)

<br>

Back in the Azure Portal ➜ erase the default text ➜ and paste the **JSON** from the GitHub link

Then click ✔️ **Done Editing** down bellow

<br>

![azure portal](https://github.com/user-attachments/assets/ed64370f-008f-4711-8e7d-25401d8a29a8)

<br>

Lastly, we'll click on the 💾 **Save** button:

- **Name the Workbook** ➜ ```linux-ssh-auth-fail```

- Make sure you select our **Log Analytics Workspace** ➜ ```LAW-Cyber-Lab```

- Place the Workbook at he same **Location** as our other Resources ➜ ```(US) East US```

Click **"Apply"**

<br>

![azure portal](https://github.com/user-attachments/assets/ed64370f-008f-4711-8e7d-25401d8a29a8)

<br>

✅ The **Workbook** and the corresponding **Sentinel Map** for the **Linux SSH Authentication Failures** were successfuully created.

<br>

![azure portal](https://github.com/user-attachments/assets/ed64370f-008f-4711-8e7d-25401d8a29a8)

<br>

We'll then continue creating the rest of the Workbooks & Maps for the rest of the Resources.

We'll click on ➕ **Add Workbook** ➜ follow the same process ➜  and use the other JSON codes from [this GitHub link](https://github.com/joshmadakor1/Cyber-Course-v2/tree/main/Sentinel-Maps(JSON))

<br>

  </details>

<br>

✅ All 4 Workbooks and Maps were successfully created:

<br>

![azure portal](https://github.com/user-attachments/assets/ed64370f-008f-4711-8e7d-25401d8a29a8)

<br>

💡 We can then Test the Query ➜ to see if Events will be plotted on the Maps.

Exit the Advanced Editor and grab the query from the main Edit page, then use it to query the logs in LAW.

For example, this is the query from the Microsoft SQL Server failed authentication workbook in LAW:





















<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>



  
> The first thing ➜ we're going to do is create a **Diagnostic Setting** in **Microsoft Entra ID**.
> 
> This will allow us to **Ingest Logs** into our **Log Analytics Workspace**.

<br>

- Choose a **"Diagnostic setting name"** ➜ I picked ```ADD-Logs```

- Under **Logs** ➜ **Category groups** ➜ select ☑️ **AuditLogs**,  ☑️ **SigninLogs** and ☑️ **NonInteractiveUserSigninLogs**

- Make sure we're sending the Logs to our **Log Analytics Workspace** ```LAW-Cyber-Lab```

Click **Save**

<br>

![azure portal](https://github.com/user-attachments/assets/ed64370f-008f-4711-8e7d-25401d8a29a8)

<br>

Next we'll create a **New User**:

- We can Name it ```Lain```

- Copy and Save the **Auto-generated Password**

<br>

![azure portal](https://github.com/user-attachments/assets/b4c7d057-a52c-4dee-bcd5-79111a5f44d6)

<br>

Go to the **Assignments** tab ➜ click on ➕ **Add role** ➜ assign the **Global Administrator** role to the New User.

Click **"Review + create"** to Create the New User:

<br>

![azure portal](https://github.com/user-attachments/assets/3e824ba8-8383-441b-9419-346b8bfab7a2)

<br>

<h2></h2>

<br>

We'll now create another **New User** ➜ this is going to be our **"Attacker" User** ```Madara```

➡️ Generate some **Failed Authentication Logs** ➜ by failing to Log In 10 times in a row.

<br>

![azure portal](https://github.com/user-attachments/assets/b5025517-7ef9-4705-b200-5ced4626b52c)

<br>

<h2></h2>

<br>

We can go back to our **Log Analytics Workspace** to confirm that **Logs are Properly Being Ingested**.

<br>

>   <details close> 
>   
> **<summary> 💡 Note</summary>**
> 
> The **AuditLogs** come in pretty quickly, but the **SigninLogs** and **AzureActivity** take a while to come into the **Log Analytics Workspace**.
>   
> Generate the logs, then take a 20-30 minute coffee break and query the LAW after.
> 
>   </details>

<br>

### Audit Logs:

<br>

![azure portal](https://github.com/user-attachments/assets/0768f8c7-814f-417a-a249-b3d684091d33)

<br>

### Signin Logs:

<br>

![azure portal](https://github.com/user-attachments/assets/cb258735-8498-4926-955c-397cdd31f603)

<br>

  </details>

<h2></h2>

<details close> 
<summary> <h2>2️⃣ Subscription Level Logging ➜ Activity Log</h2> </summary>
<br>

We're now going to export the **Azure Activity Logs** to our **Log Analytics Workspace**.

Go to **Azure Monitor** ➜ then the **Activity Log** blade ➜ and click on ⚙️ **Export Activity Logs**

<br>

![azure portal](https://github.com/user-attachments/assets/bf87437a-ba52-4a1e-9ca1-4856940e053f)

<br>

We'll then create a new **Diagnostic Setting** ➜ I named mine ```ds-activity-logs```:

<br>

![azure portal](https://github.com/user-attachments/assets/d4c4cc49-71f8-4ab9-85d9-942d80a8c289)

<br>

Now we'll **Generate some Logs** to confirm functionality.

To do so I decided to:

- Create 2 New **Resource Groups**
- Add a new **Inbound Security Rule** to 1 of the existing NSGs

<br>

### New Resource Groups:

<br>

![azure portal](https://github.com/user-attachments/assets/c1273b17-0839-4d9a-b87c-a50b3db2554b)

<br>

### New Inbound Security Rule in the ```attack-vm-nsg```:

<br>

![azure portal](https://github.com/user-attachments/assets/5d18fe9e-f39b-41a8-8665-1506fbd81758)

<br>

💡 I then Deleted all these new Resources just to confirm the **Logs were Flowing into the LAW Properly**.

Back to our **Log Analytics Workspace** ➜ I **Queried the Logs** for any **Changes to the NSGs**:

<br>

![azure portal](https://github.com/user-attachments/assets/1f7885d3-13bf-454c-8d8d-4a9e6d229666)

<br>

I also performed another **Query for Checking Resource Group Deletion** in our Logs:

<br>

![azure portal](https://github.com/user-attachments/assets/26ca75bd-e180-4e8b-9f95-858145bb805b)

<br>

  </details>

<h2></h2>

<details close> 
<summary> <h2>3️⃣ Resource Level Logging ➜ Azure Storge Account & Azure Key Vault</h2> </summary>
<br>

The next step is to Enable Logs for our Storage account and for our Key Vault.

<br>

### Storage Account:

<br>

Go to **Storage Accounts** ➜ and select our ```sacyberlab009``` Storage Account

On the left side under **Monitoring** ➜ select the **Diagnostic settings** blade

For the **"blob"** line ➜ click on ⛔ **Disabled** under **"Diagnostic status"** for the 

<br>

![azure portal](https://github.com/user-attachments/assets/14c169a9-f7cc-4c4e-8c0e-23e6f7898c9e)

<br>

Click on ➕ **Add Diagnostic setting**

<br>

![azure portal](https://github.com/user-attachments/assets/9ad6d6eb-6fcd-4208-90c6-c2f9308ad88d)

<br>

- Set up a **"Diagnostic setting name"** ➜ I picked ```ds-storage-acct```

- Under **Logs** ➜ **Category groups** ➜ select ☑️ **audit**

- Make sure we're sending the Logs to our **Log Analytics Workspace** ```LAW-Cyber-Lab```

Click **Save**

<br>

![azure portal](https://github.com/user-attachments/assets/6750ea6a-f1b8-46b5-81c2-c16358ecf292)

<br>

<h2></h2>

<br>

### Azure Key Vault:

<br>

Navigate to **Azure Key Vault** ➜ click on **"Create a Key Vault"**.

⚠️ Make sure it is in the same Resource Group & Region as our other Resources.

Also ➜ the **"Key vault name"** must be Globally Unique.

Click the **"Next"** button:

<br>

![azure portal](https://github.com/user-attachments/assets/0928b8a2-16e2-4e10-8598-2870b2f30635)

<br>

Under the **"Access configuration"** tab ➜ set the **"Permission model"** to ◉ **Vault access policy**

Click on **"Review + Create"**.

<br>

![azure portal](https://github.com/user-attachments/assets/5e84b87f-728d-498b-8ea0-e1d02b71f406)

<br>

We'll then create a **Diagnostic Setting** for the **Key Vault** ➜ the same way we did for the **Storage Account**.

<br>

![azure portal](https://github.com/user-attachments/assets/463cc82f-4806-4c1f-9103-051ab84689f8)

<br>

- Pick a **"Diagnostic setting name"** ➜ ```ds-akv```

- Under **Logs** ➜ **Category groups** ➜ select ☑️ **audit**

- Once again ➜ make sure we're sending the Logs to our **Log Analytics Workspace** ```LAW-Cyber-Lab```

Click **Save**

<br>

![azure portal](https://github.com/user-attachments/assets/358c763b-3b13-49ae-be30-ae40384df755)

<br>

  </details>

<h2></h2>

<details close> 
<summary> <h2>4️⃣ Generate some Logs</h2> </summary>
<br>

Finally, we're going to generate some logs by creating a Few Secrets inside of our Azure Key Vault

We're then going to **Query those Logs** and analyse them inside of our LAW.

<br>

### Secret Number 1:

<br>

![azure portal](https://github.com/user-attachments/assets/677d2a01-7249-4784-ba4d-14ec206b7014)

<br>

### Secret Number 2:

<br>

![azure portal](https://github.com/user-attachments/assets/93575473-1b10-46a3-8b71-ed3eb61897d3)

<br>

Inside of our ```ak-cyber-lab``` **Key Vault** ➜ we can confirm that both Secrets were Created ✅

<br>

![azure portal](https://github.com/user-attachments/assets/c03626dd-4df1-4c3a-99fe-ce8dbb007f83)

<br>

So we'll then Query our ```LAW-Cyber-Lab``` ➜ to make sure **Logs are Flowing from our Resources**:

<br>

![azure portal](https://github.com/user-attachments/assets/8a1c02ff-e3b8-48a0-ae37-b69d648bae25)

<br>

  </details>

<h2></h2>

<br>

<br>

<br>

<br>

<br>

<br>

<br>
  
<br>
