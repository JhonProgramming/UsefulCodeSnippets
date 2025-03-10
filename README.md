SQL:
sql connection string:
string connectionString = "Data Source = (LocalDB)\\MSSQLLocalDB; AttachDbFilename = file path ; Integrated Security = True; Connect Timeout = 30"; 
SqlConnection sqlConnection = new SqlConnection(connectionString);
sql command:
SqlCommand command = new SqlCommand("command name", sqlConnection); 
command.CommandType = CommandType.StoredProcedure; 
passing paramters to sql command:
command.Parameters.AddWithValue("@parameter", variable);
using insert, update, delete commads:
sqlConnection.Open(); 
command.ExecuteNonQuery(); 
sqlConnection.Close(); 
using select command (putting it into datatable):
SqlDataAdapter sd = new SqlDataAdapter(cmd);
sqlConnection.Open(); 
sd.Fill(datatable name); 
sqlConnection.Close(); 
stored procedures:
Create procedure [dbo].[procedure name] 
( 
@param1 type, 
@param2 type 
) 
as 
begin 
sql command
End 
insert:
insert into table name values @param1, @param2 
select:
select * from table name (where____ if neccessary)
delete:
Delete from table name (where___ if neccessary) 
update:
Update table name 
set column=@param1, 
column=@param2 
(where___ if neccessary)
--------------------------------------------------------------------------------------------
APIs:
private const string API_KEY = " API KEY HERE";
string Url = "http://api.openweathermap.org/data/2.5/forecast?" (<--- replace with API site url) + "q=" + city (<-- parameters) + "&mode=xml&units=metric&APPID=" + API_KEY;
getting data from API:
            // Get the response string from the URL. 
             (function-->)GetForecast(**client.DownloadString(ForecastUrl)** (<-- important bit)); 
        } 
        
        // Display the forecast. 
        private void GetForecast(string xml) 
        { 
            // Load the response into an XML document. 
            XmlDocument xmlDoc = new XmlDocument(); 
            xmlDoc.LoadXml(xml);  (<--- putting data from API into xml document)

              foreach (XmlNode timeNode in xmlDoc.SelectNodes("//time (API header thing)")) 
            { 
                // Get the time in UTC. 
                DateTime time = DateTime.Parse(timeNode.Attributes["from"].Value); 
                // Get the temperature. 
                XmlNode tempNode = timeNode.SelectSingleNode("temperature (subsection of each data entry)");
                string temp = tempNode.Attributes["value"].Value; (<--- specific bit of data from subsection)
                // Get the temperature. 
                XmlNode windSpeedNode = timeNode.SelectSingleNode("windSpeed"); 
                string windSpeed = windSpeedNode.Attributes["mps"].Value; 
                
![image](https://github.com/user-attachments/assets/bd4f5caa-f3a9-49b4-9dc7-202ca9996181)

                ^what the API data page thing looks like, useful for figuring out what to put when getting data from the xml
---------------------------------------------------------------------------------------------
general:
empty text box:
txtPeople.Text = string.Empty; 
conditionals:
if ((username==checkUser) && (password==checkPass)) <-- condition 1 AND condition 2
! <- not condition
^ <- XOR
|| <- OR
getting rows from datatable:
foreach (DataRow dr in datatablename.Rows) 
datatype variablename = (cast data type)(dr["column name"]); - regular get from datatable
string variable = dr["column"] != DBNull.Value ? (string)(dr["column"]) : "N/A"; - conditional get from datatable (gets data, if column for that row is blank, sets it as "N/A")
make sure to do anything with the data in the foreach loop
radio buttons:
private void chkTempFilter_CheckedChanged(object sender, EventArgs e) <--- event for when a radiobutton is checked / unchecked
            var TempRadioButtons = gbxTempFilters.Controls.OfType<RadioButton>();  <---- put at the top of the program, where the initialize is, gets all radiotbuttons in specified group box and stores them together
            foreach (RadioButton item in TempRadioButtons) 
            { 
                item.CheckedChanged += TempFilters_CheckedChanged; 
            } 
            
            string checkedName = ((RadioButton)sender).Name;  <-- use these in the checked change event to detect which ones are checked or not and do stuff baesd on that
            if (checkedName == "rbtnSpeedGreater") 

             if (rbtnGreaterTemp.Checked) <-- conditional based on if radiobutton is checked, works for check boxes as well

add visual basic to project:
![image](https://github.com/user-attachments/assets/0394bcbe-2493-4c7b-b7ee-cd097f5942e8)
right click on the project name, go to add, go to references, search for microsoft visual basic
string input = Interaction.InputBox("Prompt", "Title", "Default"); <-- code for input box
error handling:
try - catch - finally
try {} <- block of code
catch (exception e) {} <- block of code to do on exception catch, can specify what exception to catch and can have multiple catches for different exceptions
finally {} <- executes block after try - catch regardless of outcome
----------------------------------------------------------------------------------------------------
Multiple forms:
make second or third or fourth, etc, etc form
give it a name
CreateAccountForm create = new CreateAccountForm(); <--- put this at the top of the program to create the new forms (replace names with your own)
do this for every form you need
 private void btnLogIn_Click(object sender, EventArgs e) <- button click
 {
     if (logIn.ShowDialog() <- opens the form with the dialogue option == DialogResult.OK <- if the result on page close is OK) <- conditional using the result from the form
     {
         MessageBox.Show("Successful Log In");
         this.Hide(); <- makes the form invisible but does not close it entirely (closing the initial form1 just shuts the entire program down)
         if (main.ShowDialog() == DialogResult.OK)
         {
             this.Close(); <- fully closes the relevant form
         }
     }
 }

if (check) <- put this stuff at the end of the new form(s) code
both options close the current form down 
dont need both can just have ok or close
{ 
    this.DialogResult = DialogResult.OK; <- can be used for conditionals in the program that called the form to open
}
else
{
    this.DialogResult= DialogResult.Cancel;
}
use sql databases for transmitting data between forms (its just easier this way)
if you wanna put text in textboxes between forms use this:
public static TextBox test = new TextBox(); <- put this at the top of the code to create a textbox variable
        private void Form1_Load(object sender, EventArgs e)
        {
            test = txtTest; <- put this in the form load event and set the variable to the name of a textbox in the form
        }

        Form1.test.Text = "test"; <- put this in the other form (replacing names as neccessary) to put the text into the textbox
        same thing might work for other variables but its dubious
----------------------------------------------------------------------------
random numbers:
 private void btnRand_Click(object sender, EventArgs e)
 {
     Random rdn = new Random();
     int num = rdn.Next(0, 10); //<-- min <= random < max

     double fl = rdn.NextDouble(); //<-- stupid long decimal
     fl = Math.Truncate(10 * fl) / 10; //<-- times by x, then truncate, then divide by x to get x number of decimal places (10 for 1 dp, 100 for 2 dp, etc)
 }
-----------------------------------------------------------------------------
