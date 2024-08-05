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

![azure portal](https://github.com/user-attachments/assets/36df51b2-cdcd-42e7-ad55-d26078edda07)

<br>

<details close> 
  
**<summary> 📝 Step-by-step Guide on How to Create the Sentinel Maps Inside the Workbooks?</summary>**

<br>

We'll first create the **Workbook** & the **Map** for the ***Linux SSH Authentication Failures***

After clicking on ➕ **Add Workbook** ➜ you can see there's a Default Workbook that Sentinel made.

Click ✏️ **Edit**

<br>

![azure portal](https://github.com/user-attachments/assets/9d44e9cd-77b8-41f4-93a7-2067a752e545)

<br>

There's 2 Elements in the default workbook ➜ so we'll 🗑️ **Remove** them both

<br>

![azure portal](https://github.com/user-attachments/assets/343aafd9-44d7-4b59-bcda-b031db117d2b)

<br>

![azure portal](https://github.com/user-attachments/assets/202e60b2-e41e-4278-a423-c2b64b411707)

<br>

Then we're going to click on ➕ **Add** ➜ and we're going to 𝄜 **Add query** based element

<br>

![azure portal](https://github.com/user-attachments/assets/4ab29302-b055-44cb-ba8e-7cb881f5b0c7)

<br>

We'll then click the **</> Advanced Editor blade**

<br>

![azure portal](https://github.com/user-attachments/assets/d413801a-f244-417b-b0e1-98123d4fc183)

<br>

Now go to [this GitHub link](https://github.com/joshmadakor1/Cyber-Course-v2/blob/main/Sentinel-Maps(JSON)/linux-ssh-auth-fail.json) to get the **JSON** for the **Linux SSH Failed Authentication Map**.

Copy the **JSON** text.

<br>

![azure portal](https://github.com/user-attachments/assets/f3af9386-d113-4c36-ac3f-02f2729f170a)

<br>

Back in the Azure Portal ➜ erase the default text ➜ and paste the **JSON** from the GitHub link

Then click ✔️ **Done Editing** down bellow

<br>

![azure portal](https://github.com/user-attachments/assets/17ab1229-7a1b-46d8-bc07-a5eb7fa9069e)

<br>

Lastly, we'll click on the 💾 **Save** button:

- **Name the Workbook** ➜ ```linux-ssh-auth-fail```

- Make sure you select our **Log Analytics Workspace** ➜ ```LAW-Cyber-Lab```

- Place the Workbook at he same **Location** as our other Resources ➜ ```(US) East US```

Click **"Apply"**

<br>

![azure portal](https://github.com/user-attachments/assets/da6e470e-b63b-401d-8b97-c9d2883ad25a)

<br>

✅ The **Workbook** and the corresponding **Sentinel Map** for the **Linux SSH Authentication Failures** were successfuully created.

<br>

![azure portal](https://github.com/user-attachments/assets/63f4d693-f9a9-44b1-99cd-70b408a5b8a1)

<br>

We'll then continue creating the rest of the Workbooks & Maps for the rest of the Resources.

We'll click on ➕ **Add Workbook** ➜ follow the same process ➜  and use the other JSON codes from [this GitHub link](https://github.com/joshmadakor1/Cyber-Course-v2/tree/main/Sentinel-Maps(JSON))

<br>

  </details>

<br>

✅ All 4 Workbooks and Maps were successfully created:

<br>

![azure portal](https://github.com/user-attachments/assets/425a8c12-e647-40d9-aa56-4fa965ea75da)

<br>

<details close> 
  
**<summary> 💡 We can then Test the Query ➜ to see if Events will be plotted on the Maps.</summary>**

<br>

From inside the **Workbook** ➜ click on ✏️ **Edit** ➜ and then **↑ Edit**

<br>

![azure portal](https://github.com/user-attachments/assets/d115a623-3ec5-4584-993f-ec5ea9f48bf4)

<br>

![azure portal](https://github.com/user-attachments/assets/d5b9d372-f6b4-49f2-8674-12adb50aa0a2)

<br>

Copy the **"Log Analytics Worspace Logs Query"** from under the ⚙️ **Settings"** blade

<br>

![azure portal](https://github.com/user-attachments/assets/0c976a36-0991-4679-aea1-22588d9b24f6)

<br>

We'll then go to our Log Analytics Workspace ```LAW-Cyber-Lab``` ➜ and **Paste It** to **Query the Logs**

<br>

  </details>

<br>

For example ➜ this is the Query from the **Microsoft SQL Server Failed Authentication** Workbook in LAW:

<br>

![azure portal](https://github.com/user-attachments/assets/25d8d89c-1a6c-4158-8400-35c46995a395)

<br>

By doing this ➜ you can test changes to the Query.

This way we make sure it works and it's generating desired result ➜ before updating the Workbooks in Sentinel.

<br>

  </details>

<h2></h2>

<details close> 
<summary> <h2>2️⃣ Alert Creation</h2> </summary>
<br>



Here we're using KQL queries to trigger alerts and spin up incidents in Microsoft Sentinel.

Sentinel > Analytics > Create scheduled query rule

















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
<summary> <h2>3️⃣ Attack Traffic Generation ➜ Simulated Attacks</h2> </summary>
<br>

To test your alerts and incidents rule configuration, simulate some attacks on the VMs and see if they show up in Sentinel (generate alerts and incidents). We have to make sure these work before the first observation period. Here are some tests to run:

<br>

Trigger AAD Brute Force Success:

Simulate brute force success against Azure AD with your attacker account (from attack-vm). Either use PowerShell or an incognito window to fail 10-11 consecutive logins, followed by one successful login.

Trigger MSSQL Brute Force Attempt: Using the attack-vm, use PowerShell of SSMS to simulate brute force attempt against your SQL Server by failing 10-11 consecutive logins.

Trigger Malware Outbreak: In windows-vm generate a malware alert by using PowerShell to create 1 or more EICAR files. You can also do this manually by creating a text file with an EICAR string in it.

Trigger Possible Privilege Escalation (AKV Critical Credential Retrieval or Update): Manually read Key Vault Secret “Tenant-Global-Admin-Password” in the Azure portal.

Trigger Windows Host Firewall Tampering: Manually Enable and Disable the windows-vm Firewall.

Trigger Excessive Password Resets: Reset a users’ password in the Azure portal 10-11 times.

<br>


After each attach, wait 10-20 minutes, then check Sentinel to see if you have any incidents. This can also help you with incident investigation later on in the lab.

Incidents in Sentinel after simulating some attacks:

<br>

![azure portal](https://github.com/user-attachments/assets/5d18fe9e-f39b-41a8-8665-1506fbd81758)

<br>


<br>


<br>


<br>


<br>


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
