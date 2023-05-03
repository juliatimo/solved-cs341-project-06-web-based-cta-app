Download Link: https://assignmentchef.com/product/solved-cs341-project-06-web-based-cta-app
<br>
The goal of Project #06 is to extend an existing web app that retrieves information about CTA L stations and stops.  A working application is provided that does 3 things:

<ol>

 <li>Tests the database connection</li>

 <li>Retrieves information about CTA stations</li>

 <li>Displays total CTA ridership by month</li>

</ol>

The app is based on the MVC design pattern, using ASP.NET, C# and ADO.NET.  You must work within this design by extending / creating Views and Models.  To run the provided application, login to Codio and open <strong>project 06</strong>.  Then open a terminal window, change directory to “cta-web”, and “dotnet run” to start a web server (<em>Kestrel</em>) and load the web app:

The web server is now running, waiting for clients to connect via a web browser.  The simplest way to connect is via the “Box URL” command in the next to last menu in Codio.  Drop the menu and select “Box URL”:

The “Box URL” command will browse to the web app and trigger the loading of the home page:

Click on “Connection” to check the connection status to the Azure CTA database.  Then click “Station Info”, and you’ll be asked to enter a full or partial station name:

Enter “lake” and click lookup.  This will retrieve information about 5 stations, in alphabetical order by station name:

Finally, click “Ridership by Month”.  This will produce a graph of total ridership across the CTA L system, by month (next page):

<h1>CTA Database</h1>

We are working with the CTA database running in Azure.  The following is a diagram of the tables in the database.

<h1>Assignment</h1>

The assignment is to extend the given web application in the following ways:

<ol>

 <li>Modify the existing “About” view and model to display something about yourself.</li>

 <li>Modify the existing “Contact” view and model to display some sort of contact info (your name or netid is sufficient).</li>

 <li>Extend the existing “Station Info” view and model by adding 2 more columns of information: # of stops (integer), and how many of these stops are handicap accessible (string value that’s either “none”, “some”, or “all”).  Note that information about handicap accessibility is stored in the ADA column of the Stops table (0 means no, 1 means yes).  You are required to extend the <strong>Station</strong> class to store this additional information, which the view then retrieves and displays.</li>

</ol>

[ NOTE:  “Station Info” involves 2 views, <strong>GetStationInput</strong> to obtain the station name and

<strong>StationInfo</strong> to display the actual information.  The corresponding models are

<strong>GetStationInputModel</strong> and <strong>StationInfoModel</strong>, along with the <strong>Station</strong> class. ]

<ol start="4">

 <li>Add a “Lines” view and model to display information about the Stations along a particular Line. The user will enter a Line name and then information about all the stations along that will be displayed.  For each station, display the station id, the station name, and the number of stops (entrances) associated with that station in the order that the stations are visited along that line.  You are required to define a <strong>Line</strong> class to properly model the information about the line.</li>

</ol>

[ NOTE: follow the same design as “Station Info”, i.e. using one model to contain the information about the Line including the list of Station models, and a new view for the Station model. ]

<ol start="5">

 <li>Add a “Ridership by Day” view and model. Follow the “Ridership by Month” example, instead grouping the results by which day of the week (Monday, Tuesday, etc.).  You can use the DATENAME(WEEKDAY, Date) function to extract the day of the week from the Date field.</li>

 <li>Add something of your own choice. Suggestions include “Top-10 Stations by Ridership”, or viewing ridership by the different days of the week (W vs. A vs. U), or graphing ridership for a particular station by month or year.</li>

</ol>

You should plan to work on <strong>Codio</strong> since this is how submissions will be collected (we will not be using Gradescope for this project, nor Blackboard).  You can work in outside Codio if you want, but then you’ll need to upload your final project to Codio for submission.  To work in <em>Visual Studio for Windows</em> you’ll need to first run <em>Visual Studio Installer</em> to add the ASP.NET workload.  Then you can login to Codio, export the provided files to your local system, unzip, and then open the provided .csproj file.

You should then be able to run (F5) from within Visual Studio.

<h1>Getting Started with ASP.NET</h1>

<strong>ASP</strong> stands for “Active Server Pages”, and the <strong>.NET</strong> refers to the .NET family of languages:  C#, F#, VB, etc.

Most web apps today using a combination of technologies, in our case you can think of ASP.NET =&gt; HTML + C#.  This is a server-side technology, which means that

<ol>

 <li>The user (“client”) uses a browser to request a web page — from any platform, using any browser</li>

 <li>The web server (“server”) loads the web page (in our case a mix of HTML and C#), executes the C# to produce more HTML, and returns pure HTML to the client</li>

</ol>

At this point the client-server interaction is done; the user might request another web page from this site, or surf away to another web site.  A simplified visual is shown to the right.  The difference is that where you see “read file”, think “read file and execute C#”.

Since web applications have a very different architecture, we are providing a working application to help you get started.  Since there are many moving parts to a MVC-based solution, you’ll need to learn your way around app.

<ol>

 <li>Login to Codio</li>

 <li>There are 2 folders: “cta-web” is the provided web app, “__save” is a backup copy.</li>

 <li>Run the provided app:</li>

</ol>

cd cta-web

<ol start="4">

 <li>Stop and reflect for a second… The database (our data store) is running in Azure.  Our web app (our data access and logic tiers) is running in Codio.  But a web app requires a web server, so that is *also* what we’re running when we say dotnet run — we are starting a web server (Kestrel), which in turn is hosting our web app (CTA).  That’s why you must leave the program running in Codio while you run and test your web app.  When you need to make changes to your web app, you’ll stop the web server by typing Ctrl+C in the terminal window.</li>

 <li>Assuming the web server is running, the last step is to browse to your web app. In theory your Codio</li>

</ol>

VM is public on the internet, but in reality (due to security concerns) it can only be accessed by you.  In particular, it can only be accessed by the browser you have open, since this is the only one that has login credentials to access Codio.  The easiest way to access your web app is to use Codio’s “access” menu, which is the next to last menu in Codio:

Drop the menu and select “Box URL” — this should open a new tab in your browser, and automatically surf to the web app you have running.  The first time you’ll see a “cookie” dialog across the top, which you should accept.  Then you’ll see the web app’s home page with a menu bar above:

<ul>

 <li>At this point, all is well and you have a working web app that you can extend. Close the browser tab containing this web page, and then stop the web server by clicking in the terminal window and pressing Ctrl+C.</li>

</ul>

<strong><u>NOTE</u></strong>:  if you take a break or walk away from Codio for an extended period of time, the Codio system will timeout and your login credentials will expire.  If you find yourself in a situation where the web app does not open, the solution is to logout of Codio, close the browser, reopen the browser, and log back into Codio.  Then all should be well.

<ol start="7">

 <li>As discussed earlier, the web app is using a Model-View-Controller architecture, where the Controller portion is supplied. Our job is to provide the Models and Views that constitute our app.</li>

 <li>For example, open the Views sub-folder. The home page is represented by the view “Index.cshtml”.  Double-click and open this file in the editor:</li>

</ol>

<strong>@page </strong>

<strong>@model IndexModel </strong>

<strong>@{ </strong>

<strong>    ViewData[“Title”] = “Home page”; </strong>

<strong>  &lt;h2&gt;Information about CTA L stations and stops&lt;/h2&gt; } </strong>

The first line tells ASP.NET that this file contains a web page (and hence ASP.NET should build a

controller to handle requests for this page).  The second line says there is an underlying model to potentially supply data to this page.  The rest of the file should contain HTML, or a mix of HTML and C#.  To mix HTML and C#, you surround with @{ … }, as shown above.  [ <u>NOTE</u>: to comment out “code” in a view, surround with @* … *@ ]

<ol start="9">

 <li>The home page (“Index.cshtml”) refers to a model on line 2. By convention, the underlying model is stored in the Models sub-folder, in a file named “Index.cshtml.cs”. The file *must* contain a C# class named <strong>IndexModel</strong> (as defined on line 2).  The purpose of the model is to supply data needed by the web page, e.g. when the user “gets” the page:</li>

</ol>

using System;

using System.Collections.Generic; using System.Linq; using System.Threading.Tasks; using Microsoft.AspNetCore.Mvc;

using Microsoft.AspNetCore.Mvc.RazorPages;

namespace program.Pages

{

public class <strong>IndexModel</strong> : PageModel

{

public void <strong>OnGet</strong>()

{

// nothing to do — home page has no app-specific data:

}

}

}




When the home page is first loaded, the controller will called the OnGet() function to obtain any data needed by the page.  In this case no data is needed, so the function is empty.

<ol start="10">

 <li>Next, take a look at the View “Connection.cshtml”, which displays the current status of the database connection:</li>

</ol>

<strong>@page </strong>

<strong>@model ConnectionModel </strong>

<strong>@{ </strong>

<strong>  ViewData[“Title”] = “Connection to Database”; </strong>

<strong>  &lt;h1&gt;@Model.Status&lt;/h1&gt; </strong>

<strong>} </strong>

Notice the view refers to @Model.Status, i.e. the <strong>Status</strong> data member of the associated model ConnectionModel.  You’ll find that in the Model “Connection.cshtml.cs”:

using System;

using System.Collections.Generic;   using System.Linq;   using System.Threading.Tasks;   using Microsoft.AspNetCore.Mvc;   using Microsoft.AspNetCore.Mvc.RazorPages;

namespace program.Pages

{

public class <strong>ConnectionModel</strong> : PageModel

{

public string <strong>Status</strong> { get; set; }




public void <strong>OnGet</strong>()

{

if ( DataAccessTier.DB.TestConnection() )         Status = “Database connection status: good”;

else

Status = “Database connection status: unreachable”;

}

}

}




In this case the model uses the <strong>DataAccessTier</strong> to ping the database, and reports the result via updating the <strong>Status</strong> data member.




<ol start="11">

 <li>Okay, here’s a more interesting example: “Station Info”. Displaying station information is a two-step process.  First the view “GetStationInput” is displayed to obtain input from the user:</li>

</ol>

Let’s look at the underlying view in detail (you may need to read this section a few times).  This is the view “GetStationInput.cshtml”:

@page

@model <strong>GetStationInputModel</strong>

@{

ViewData[“Title”] = “Get Station Input”;

}




&lt;div class=”container”&gt;

&lt;h2&gt;Which stations(s) are you interested in?&lt;/h2&gt;

&lt;hr /&gt;

&lt;br /&gt;

<strong>&lt;form action=”StationInfo” method=”get”&gt; </strong>




&lt;div class=”row”&gt;

&lt;div class=”col-md-4″&gt;

<strong>            &lt;label asp-for=”Input”&gt;Enter station name (full or partial):&lt;/label&gt;   </strong>

<strong>            &lt;input asp-for=”Input” class=”form-control” /&gt;   </strong>

&lt;/div&gt;

&lt;/div&gt;




&lt;br /&gt;

&lt;input type=”submit” value=”Lookup” class=”btn btn-primary” /&gt;

&lt;a class=”btn btn-default” href=”/”&gt;Cancel&lt;/a&gt;




&lt;/form&gt;

&lt;/div&gt;

The important lines are 11, and 15-16.  Line 11 specifies that when the form is submitted (by clicking the Lookup button), the action will be to “get” the “StationInfo” view.  Lines 15-16 associate the user’s input with a model variable called “Input” (capitalization is important), and causes this “Input” to be passed as a URL parameter when the “get” occurs.  Here’s the underlying model in “GetStationInput.cshtml.cs, which must specify “Input” as a public data member:

namespace program.Pages

{

public class <strong>GetStationInputModel</strong> : PageModel

{

public string <strong>Input</strong> { get; set; }




public void <strong>OnGet</strong>()

{

// no data needed for initial view:

}




}//class

}//namespace

When the user clicks <strong>Lookup</strong>, the web app will get the “StationInfo” view and pass the input along.  Here’s what that final web page looks like:

Here’s the underlying view “StationInfo.cshtml”, which displays the simple data members are simple HTML, displays exception info if one occurred, and displays the list of stations using a table:

@page

@model StationInfoModel

@{

ViewData[“Title”] = “Station Information”;

}




&lt;h2&gt;Station Information&lt;/h2&gt;




&lt;br /&gt;

Your search string: “<strong>@Model.Input</strong>”

&lt;br /&gt;

# of stations found: <strong>@Model.StationList.Count</strong>

&lt;br /&gt;

&lt;br /&gt; @{

if (<strong>@Model.EX</strong> != null)

{

&lt;h3&gt;**ERROR: <strong>@Model.EX.Message</strong>&lt;/h3&gt;

&lt;br /&gt; &lt;hr /&gt; &lt;br /&gt; &lt;br /&gt;

}

}




&lt;table class=”table”&gt;

&lt;thead&gt;

&lt;tr&gt;

&lt;th&gt;

ID

&lt;/th&gt;

&lt;th&gt;

Name

&lt;/th&gt;

&lt;th&gt;

Average Daily Ridership

&lt;/th&gt;

&lt;/tr&gt;

&lt;/thead&gt;

&lt;tbody&gt;

@<strong>foreach (var item in Model.StationList)</strong>

{

&lt;tr&gt;

&lt;td&gt;

<strong>@item.StationID </strong>

&lt;/td&gt;

&lt;td&gt;

<strong>@item.StationName </strong>

&lt;/td&gt;

&lt;td&gt;

<strong>@item.AvgDailyRidership </strong>

&lt;/td&gt;

&lt;/tr&gt;

}

&lt;/tbody&gt;

&lt;/table&gt;

The associated Model in “StationInfo.cshtml.cs” is the C#, ADO.NET and SQL code needed to retrieve the necessary station data from the CTA database and turn this data into a list of Station objects.  Here’s the code

using System;

using System.Collections.Generic;   using System.Linq;   using System.Threading.Tasks;   using Microsoft.AspNetCore.Mvc;   using Microsoft.AspNetCore.Mvc.RazorPages;   using System.Data;




namespace program.Pages

{       public class StationInfoModel : PageModel

{      public List&lt;Models.Station&gt; <strong>StationList</strong> { get; set; }    public string <strong>Input</strong> { get; set; }    public Exception <strong>EX</strong> { get; set; }

public void <strong>OnGet</strong>(string input)

{

StationList = new List&lt;Models.Station&gt;();




// make input available to web page:

Input = input;




// clear exception:

EX = null;

<strong>try </strong>

{

// Do we have an input argument?  If not, there’s nothing to do:

if (input == null)

{

// there’s no page argument, perhaps user surfed to the page directly?

}

else

{

// Lookup station(s) based on input, which could be id or a partial name:      string sql;




// lookup station(s) by partial name match:

input = input.Replace(“‘”, “””);




sql = string.Format(@”

SELECT Stations.StationID, Stations.Name, AVG(DailyTotal) AS AvgDailyRidership  FROM Stations

LEFT JOIN Riderships ON Stations.StationID = Riderships.StationID

WHERE Stations.Name LIKE ‘%{0}%’

GROUP BY Stations.StationID, Stations.Name

ORDER BY Stations.Name ASC;

“, input);




DataSet ds = <strong>DataAccessTier.DB.ExecuteNonScalarQuery</strong>(sql);




<strong>foreach</strong> (DataRow row in ds.Tables[0].Rows)

{

Models.Station s = new Models.Station();




s.StationID = Convert.ToInt32(row[“StationID”]);

s.StationName = Convert.ToString(row[“Name”]);




// avg could be null if there is no ridership data:       if (row[“AvgDailyRidership”] == System.DBNull.Value)        s.AvgDailyRidership = 0;

else

s.AvgDailyRidership = Convert.ToInt32(row[“AvgDailyRidership”]);

StationList.Add(s);

}

}//else

}

<strong>catch</strong>(Exception ex)

{

EX = ex;

}

<strong>finally </strong>

{

// nothing at the moment

}

}




}//class

}//namespace







<ol start="12">

 <li>There’s a lot going on in the above Views and Models, you may need to re-read a few times… Where’s the <strong>Station</strong> class?  In “Station.cs” in Models.  You’ll want to review that class as well.</li>

</ol>




<ol start="13">

 <li>Interestingly, where is the menu defined that appears across the top of the web page?</li>

</ol>










Under Views, expand the folder “Shared”.  Open the file “_Layout.cshtml”.  In the file you’ll see a &lt;div&gt; tag with class=“navbar-collapse collapse”:




&lt;div class=”navbar-collapse collapse”&gt;

&lt;ul class=”nav navbar-nav”&gt;

<strong>                   &lt;li&gt;&lt;a asp-page=”/Index”&gt;Home&lt;/a&gt;&lt;/li&gt; </strong>

<strong>                   &lt;li&gt;&lt;a asp-page=”/Connection”&gt;Connection&lt;/a&gt;&lt;/li&gt; </strong>

<strong>                   &lt;li&gt;&lt;a asp-page=”/GetStationInput”&gt;Station Info&lt;/a&gt;&lt;/li&gt; </strong>

<strong>                   &lt;li&gt;&lt;a asp-page=”/RidershipByMonth”&gt;Ridership by Month&lt;/a&gt;&lt;/li&gt; </strong>

<strong>                   &lt;li&gt;&lt;a asp-page=”/About”&gt;About&lt;/a&gt;&lt;/li&gt; </strong>

<strong>                   &lt;li&gt;&lt;a asp-page=”/Contact”&gt;Contact&lt;/a&gt;&lt;/li&gt; </strong>

&lt;/ul&gt;

&lt;/div&gt;




Notice the asp-page attribute refers to the View name, e.g. “/Connection” or “/GetStationInput”.  When the user clicks the displayed text, e.g. “Connection” or “Station Info”, this is how ASP.NET knows which View to load.  When you want to add items to the menu, you’ll add them here.




<ol start="14">

 <li>When it comes time to add features to your web app, feel free to copy existing View and Model files and modify (aka copy-paste). This is a necessary evil as you learn your way around.</li>

</ol>




<h1>Debugging</h1>

Debugging is hard in web apps since the C# code runs on the server — e.g. output from

System.Console.WriteLine is not visible.  One approach is to print debug to your web page:  add data members to the model, and then display these data members in the view using HTML and C#:




<strong>&lt;br /&gt; </strong>

<strong>Data member contains:  @Model.NameOfDataMember &lt;br /&gt; </strong>




For an example, review how the Connection view and Connection model work together to display the status of the database connection.