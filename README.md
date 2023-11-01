Create a web application to display "Welcome to the world of ASP.NET" on web browser when 
user "Click" button is clicked.
-----------------------------------------------------------------------------------------

<asp:Label ID="lblMessage" runat="server" Text="Welcome to the world of ASP.NET" />
<asp:Button ID="btnShowMessage" runat="server" Text="Show Message" OnClick="btnShowMessage_Click" />


aspx.cs file 
------------
protected void btnShowMessage_Click(object sender, EventArgs e)
{
    lblMessage.Text = "Welcome to the world of ASP.NET";
}

2)Create a web page in which user can enter enrollment no, student name and marks of 5 subjects. 
Calculate total, percentage and grade of student and display it. [Use text box, label, button control].
--------------------------------------------------------------------------------------------------------

<div>
    <h2>Student Result Calculator</h2>
    <asp:Label ID="lblEnrollmentNo" runat="server" Text="Enrollment No: "></asp:Label>
    <asp:TextBox ID="txtEnrollmentNo" runat="server"></asp:TextBox>
    <br /><br />

    <asp:Label ID="lblStudentName" runat="server" Text="Student Name: "></asp:Label>
    <asp:TextBox ID="txtStudentName" runat="server"></asp:TextBox>
    <br /><br />

    <asp:Label ID="lblSubject1" runat="server" Text="Subject 1 Marks: "></asp:Label>
    <asp:TextBox ID="txtSubject1" runat="server"></asp:TextBox>
    <br /><br />

    <!-- Repeat the above lines for Subject 2 to Subject 5 -->

    <asp:Button ID="btnCalculate" runat="server" Text="Calculate" OnClick="btnCalculate_Click" />
    <br /><br />

    <asp:Label ID="lblResult" runat="server" Text=""></asp:Label>
</div>

------------------------
form.cs file 

protected void btnCalculate_Click(object sender, EventArgs e)
{
    // Get the values from textboxes
    string enrollmentNo = txtEnrollmentNo.Text;
    string studentName = txtStudentName.Text;
    double subject1 = Convert.ToDouble(txtSubject1.Text);
    
    // Repeat the above line to get marks for Subject 2 to Subject 5

    // Calculate the total and percentage
    double totalMarks = subject1 + subject2 + subject3 + subject4 + subject5;
    double percentage = (totalMarks / 500) * 100;

    // Determine the grade based on the percentage
    string grade = GetGrade(percentage);

    // Display the result
    lblResult.Text = $"Enrollment No: {enrollmentNo}<br />" +
                    $"Student Name: {studentName}<br />" +
                    $"Total Marks: {totalMarks}<br />" +
                    $"Percentage: {percentage:F2}%<br />" +
                    $"Grade: {grade}";
}

private string GetGrade(double percentage)
{
    if (percentage >= 90)
    {
        return "A+";
    }
    else if (percentage >= 80)
    {
        return "A";
    }
    else if (percentage >= 70)
    {
        return "B";
    }
    else if (percentage >= 60)
    {
        return "C";
    }
    else if (percentage >= 50)
    {
        return "D";
    }
    else
    {
        return "F";
    }
}
-----------------------------------------------------------------------------------

3)Write a program to enable - disable textbox and change width of text box programmatically

<asp:TextBox ID="txtDynamic" runat="server" Text="Dynamic TextBox" Width="200px" Enabled="true"></asp:TextBox>
<br />
<asp:Button ID="btnEnable" runat="server" Text="Enable" OnClick="btnEnable_Click" />
<asp:Button ID="btnDisable" runat="server" Text="Disable" OnClick="btnDisable_Click" />


-------------------
form.cs file 

protected void btnEnable_Click(object sender, EventArgs e)
{
    txtDynamic.Enabled = true;
    txtDynamic.Width = 200;
}

protected void btnDisable_Click(object sender, EventArgs e)
{
    txtDynamic.Enabled = false;
    txtDynamic.Width = 100;
}

-----------------------------------------------------------------------------------

4)Create a web page that will take two radio buttons labeled as a gender, if user selects radio button 
the gender will be changed according to selected radio button.

<asp:RadioButtonList ID="rblGender" runat="server">
    <asp:ListItem Text="Male" Value="Male" />
    <asp:ListItem Text="Female" Value="Female" />
</asp:RadioButtonList>

<br />

<asp:Button ID="btnSubmit" runat="server" Text="Submit" OnClick="btnSubmit_Click" />

<br />

<asp:Label ID="lblResult" runat="server" Text="Selected Gender: " />

--------------------

protected void btnSubmit_Click(object sender, EventArgs e)
{
    string selectedGender = rblGender.SelectedItem.Text;
	
    lblResult.Text = "Selected Gender: " + selectedGender;
}

-------------------------------------------------------------------------------------

5)Write a program which have list box and image controls, list box is used to display items and when 
user clicks on item in list box it display the item image in image control.


<asp:ListBox ID="lstItems" runat="server" AutoPostBack="true" OnSelectedIndexChanged="lstItems_SelectedIndexChanged">
    <asp:ListItem Text="Item 1" Value="item1" />
    <asp:ListItem Text="Item 2" Value="item2" />
    <asp:ListItem Text="Item 3" Value="item3" />
</asp:ListBox>

<br />

<asp:Image ID="imgItem" runat="server" Height="200" Width="200" />


form.cs file 

protected void lstItems_SelectedIndexChanged(object sender, EventArgs e)
{
    string selectedItemValue = lstItems.SelectedValue;
    string imageUrl = $"~/Images/{selectedItemValue}.jpg"; // Specify the path to your image folder

    imgItem.ImageUrl = imageUrl;
}

-----------------------------------------------------------------

6) Write a program that has a form taking the user's name as input. Store this name in a permanent 
cookie & whenever the page is opened again, then value of the name field should be attached with 
the cookie's content.

<asp:TextBox ID="txtName" runat="server"></asp:TextBox>
<asp:Button ID="btnSave" runat="server" Text="Save Name" OnClick="btnSave_Click" />


form.cs file
protected void Page_Load(object sender, EventArgs e)
{
    if (!IsPostBack)
    {
        // Check if the cookie exists and has a value
        if (Request.Cookies["UserName"] != null && !string.IsNullOrEmpty(Request.Cookies["UserName"].Value))
        {
            txtName.Text = Request.Cookies["UserName"].Value;
        }
    }
}

protected void btnSave_Click(object sender, EventArgs e)
{
    string userName = txtName.Text;

    // Create a new permanent cookie and set its value
    HttpCookie cookie = new HttpCookie("UserName");
    cookie.Value = userName;
    cookie.Expires = DateTime.Now.AddYears(1); // Set the expiration date to one year from now

    // Add the cookie to the response
    Response.Cookies.Add(cookie);
}


-------------------------------------------------------------------

7)Write a program to check the length of the string in the text box using custom validation

<asp:TextBox ID="txtInput" runat="server"></asp:TextBox>
<asp:CustomValidator ID="customValidator" runat="server" ControlToValidate="txtInput"
    ErrorMessage="The input must be between 5 and 10 characters."
    OnServerValidate="customValidator_ServerValidate" Display="Dynamic" ForeColor="Red" />

<asp:Button ID="btnSubmit" runat="server" Text="Submit" OnClick="btnSubmit_Click" />


form.cs 

protected void customValidator_ServerValidate(object source, ServerValidateEventArgs args)
{
    string input = args.Value;
    int minLength = 5;
    int maxLength = 10;

    if (input.Length >= minLength && input.Length <= maxLength)
    {
        args.IsValid = true;
    }
    else
    {
        args.IsValid = false;
    }
}

protected void btnSubmit_Click(object sender, EventArgs e)
{
    if (Page.IsValid)
    {
        // The input is valid, perform the desired action
        // For example, display a message or process the input.
        // In this example, we'll display a message.
        lblMessage.Text = "Input is valid and has a length within the specified range.";
    }
}
'

-----------------------------------------------------------------------------------

Create a master page that contain links for home page, about us page and contact page, when 
user clicks on particular link it will display that particular page.


<ul>
    <li><a href="Default.aspx">Home</a></li>
    <li><a href="AboutUs.aspx">About Us</a></li>
    <li><a href="Contact.aspx">Contact</a></li>
</ul>
<asp:ContentPlaceHolder ID="ContentPlaceHolder1" runat="server">
</asp:ContentPlaceHolder>
