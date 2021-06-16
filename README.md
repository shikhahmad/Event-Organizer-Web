# Event-Organizer-Web
# Controller
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;
using Event_Management_Website.context;

namespace Event_Management_Website.Controllers
{
    public class EventController : Controller
    {
        // GET: Event
        EventManagementEntities db = new EventManagementEntities();
        public ActionResult Event()
        {

            ViewBag.Message = "Registered successfully";
            return View();
        }
        [HttpPost]
        public ActionResult AddEvent(Event_detail model)
        {
            Event_detail obj = new Event_detail();

            obj.First_Name = model.First_Name;
            obj.Last_Name = model.Last_Name;
            obj.Phone = model.Phone;
            obj.Address = model.Address;
            obj.Event_Details = model.Event_Details;
            obj.Date = model.Date;

            db.Event_detail.Add(obj);
            db.SaveChanges();

            ViewBag.Message = "Registered successfully";
            return View();
        }
        public ActionResult EventList()
        {
            var res = db.Event_detail.ToList();
            return View(res);
        }
        

    }
}

# Views
# View Registration

@model Event_Management_Website.context.Event_detail
@{
    ViewBag.Title = "Event";
}

<h2>Event Managment System</h2>


<div class="page-header">
    <h2 style="font-weight: bold;">Event Management Registeration Form</h2>
</div>

@using (Html.BeginForm("AddEvent", "Event", FormMethod.Post))
{
    <div class="container">
        <div class="form-group">
            <label> First Name </label>
            @Html.TextAreaFor(x => x.First_Name, new { @class = "form-control" })
        </div>
        <div class="form-group">

            <label> Last Name </label>
            @Html.TextAreaFor(x => x.Last_Name, new { @class = "form-control" })
        </div>
        <div class="form-group">

            <label> Phone </label>
            @Html.TextAreaFor(x => x.Phone, new { @class = "form-control" })
        </div>

        <div class="form-group">

            <label> Address </label>
            @Html.TextAreaFor(x => x.Address, new { @class = "form-control", rows = 10 })
        </div>
        <div class="form-group">

            <label> Email  </label>
            @Html.TextAreaFor(x => x.email, new { @class = "form-control" })
        </div>

        <div class="form-group">

            <label> Event Details  </label>
            @Html.TextAreaFor(x => x.Event_Details, new { @class = "form-control", row = 5 })
        </div>
        <div class="form-group">

            <label> Date  </label>
            @Html.TextAreaFor(x => x.Date, new { @class = "form-control" })
        </div>

        <div class="form-group">

            <button type="submit" class="btn btn-primary"> Submit </button>
            <button type="submit" class="btn btn-danger"> Reset </button>

        </div> 



    </div>

}

# View
# View List

@model List<Event_Management_Website.context.Event_detail>
@{
    ViewBag.Title = "EventList";
}

<h2>EventList</h2>

<table class="table table-hover">
    <tr>
        <th>First Name </th>
        <th>Last Name</th>
        <th>Phone</th>
        <th>Address</th>
        <th>Email</th>
        <th>Event Details</th>
        <th> Date</th>

    </tr>
    @foreach (var item in Model)
    {
        <tr>

            <td>
                @item.First_Name
            </td>
            <td>
                @item.Last_Name
            </td>
            <td>
                @item.Phone
            </td>
            <td>
                @item.Address

            </td>
            <td>
                @item.email
            </td>
            <td>
                @item.Event_Details
            </td>
            <td>
                @item.Date
            </td>
            <td>
                <a href="#"> <i class="glyphicon glyphicon-pencil"> </i> </a>

                <a href="#"> <i class="glyphicon glyphicon-trash"> </i> </a>
            </td>
        </tr>
        

    }

</table>

# Model
# Model contains the Database SQL Table, we have integrated the SQL Databse to the model layer
