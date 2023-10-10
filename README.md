# Abstract
The following project presents an in-depth analysis of a Supply Chain Management System, exploring its various components and their interactions. Through data analysis, visualization, and machine learning techniques, this project aims to enhance understanding and decision-making within the supply chain domain. The project offering insights into the potential improvements in efficiency, customer satisfaction, and overall operational effectiveness.

# Scope 
The Supply Chain Management System project encompasses the development and implementation of a comprehensive digital platform that streamlines the end-to-end supply chain processes. This includes order management, inventory tracking, supplier collaboration, demand forecasting, and logistics optimization.

# Objectives
-	Analyse the existing supply chain processes to identify opportunities for improvement.
-	Implement data preprocessing techniques to ensure data accuracy and consistency for analysis.
-	Utilize visualization tools like Tableau to create insightful dashboards for monitoring key supply chain metrics.
-	Apply hypothesis testing to validate the effectiveness of process optimizations and improvements.
-	Segment customers based on order history and preferences to tailor supply chain strategies.
-	Perform ABC analysis to prioritize products based on their impact on overall supply chain performance.
-	Build machine learning models that predict the likelihood of late deliveries through a website build using Flask, HTML and CSS then deployed it on AWS EC2 instance.

# Tableau Dashboard
<div class='tableauPlaceholder' id='viz1694180911303' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Sa&#47;SalesReport_16925513303360&#47;Dashboard&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='path' value='views&#47;SalesReport_16925513303360&#47;Dashboard?:language=en-US&amp;:embed=true&amp;publish=yes' /> <param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Sa&#47;SalesReport_16925513303360&#47;Dashboard&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /><param name='filter' value='publish=yes' /></object></div>

# Link
Tableau Public Link is [here](https://public.tableau.com/views/SalesReport_16925513303360/Dashboard?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link).

# Deployment on AWS EC2

1) To create an EC2 instance with Ubuntu 22.04 (free tier) and configure the security group:

   a) Use the AWS Management Console to launch an EC2 instance with Ubuntu 22.04. During setup, configure the security group with the following rules:
   
      i) Default security group rules.
      
      ii) Allow incoming traffic on ports 80 (HTTP) and 443 (HTTPS) from the internet by checking the appropriate checkboxes.
   
   b) Create and download a new key pair during the EC2 instance setup process.

2) Download Putty for the command-line interface and WinSCP for file transfer.

3) In WinSCP's login window:

   - Hostname: Use the public DNS of your EC2 instance, e.g., ec2-3-111-188-202.ap-south-1.compute.amazonaws.com.
   - Username: Enter the username from the EC2 instance connect window.
   - Password: In the advanced settings, specify the private key file (.ppk) for authentication.

4) Modify your Python code to allow external access:

   Old:
   ```python
   if __name__ == '__main__':
       app.run(debug=True)
   ```

   Updated:
   ```python
   if __name__ == '__main__':
       app.run(host='0.0.0.0', port=8080)
   ```

5) Use WinSCP to upload the required files from your computer to the Linux system on AWS.

6) Open Putty from WinSCP to establish a command-line connection without credential requirements.

7) Run the following commands in sequence within the Putty terminal:

   ```
   sudo apt install python3
   sudo apt-get update && sudo apt-get install python3-pip
   pip3 install -r requirements.txt
   python3 app.py
   ```

8) Add an inbound rule for port 8080 to allow external access:

   - Go to your EC2 instance settings, Security Groups.
   - Double-click on the security group associated with your instance.
   - Edit inbound rules and add a custom TCP rule for port 8080 with the source set to "0.0.0.0/0."
   - Save the rules.

9) Access your website using the public IPv4 address and port 8080.

10) Note that Flask is using the development server.

11) To run the Flask app in the background and avoid it stopping when you close the CLI:

    ```
    screen -R deploy python3 app.py
    ```

12) To stop a process running in a "screen" session:

    - List active "screen" sessions:
      ```
      screen -ls
      ```

    - Attach to the desired session (replace "deploy" with the actual session name if different):
      ```
      screen -r deploy
      ```

    - Stop the process by pressing CTRL + C inside the "screen" session. This terminates the running Flask App website server.
