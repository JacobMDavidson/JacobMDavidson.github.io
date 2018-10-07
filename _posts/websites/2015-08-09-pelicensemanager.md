---
layout: post
title: PE License Manager
description: "Pelicensemanager.com was the first real project I developed. By calling it a real project, I mean that it’s much more involved than developing a static website, or designing a template for a popular CMS. This project required database design, extensive PHP development, and several MySQL queries. This was a complicated project, made even more complex by my lack of knowledge and experience at the time. As it stands, pelicensemanager.com meets all requirements and functionality that I set for a minimum viable product. Now that I have more experience, the myriad of inefficiencies in the PHP code and MySQL queries are obvious, but these inefficiencies do not adversely affect usability for the current user base. It does not make sense to spend time correcting these inefficiencies until the size of the user base dictates that it is necessary. This project analysis will outline how pelicensemanager.com was constructed, and will detail the changes I would make if I revisited this project today."
modified: 2015-08-09
tags: [website, joomla]
comments: false
image:
  feature: pelicense/pelicense_banner.png
---
<figure style="text-align: center">
    <img src="{{ site.url }}/images/pelicense/pelicensemanager.jpg" alt="">
</figure>

## Summary

Pelicensemanager.com was the first *real* project I developed. By calling it a real project, I mean that it’s much more involved than developing a static website, or designing a template for a popular CMS. This project required database design, extensive PHP development, and several MySQL queries. This was a complicated project, made even more complex by my lack of knowledge and experience at the time. As it stands, pelicensemanager.com meets all requirements and functionality that I set for a minimum viable product. Now that I have more experience, the myriad of inefficiencies in the PHP code and MySQL queries are obvious, but these inefficiencies do not adversely affect usability for the current user base. It does not make sense to spend time correcting these inefficiencies until the size of the user base dictates that it is necessary. This project analysis will outline how pelicensemanager.com was constructed, and will detail the changes I would make if I revisited this project today.

## The Problem

I’m both a licensed professional engineer (PE) and a licensed structural engineer (SE). At my peak, I held 15 licenses within the United States, and managing these licenses was a complete nightmare. Not only did I have to worry about staggered expiration dates (some expired in even numbered years, some in odd numbered years, some every year, others every three years, and the expiration month varied from state to state), but I also had to manage varying continuing education requirements. The required amount, definitions, and rules of continuing education varied widely from state to state. To better illuminate this confusion, I’ll list the requirements for four separate licenses: Alabama PE, Illinois PE, Illinois SE, and Florida PE. Please note: these lists are not exhaustive. They’re simple summaries with just enough detail to depict the differences from license to license.

* *Alabama PE* – Licenses expire annually on December 31st. Fifteen professional development hours (PDHs) are required annually, and a maximum of 15 PDHs may be carried over from the previous period.
* *Illinois PE* – Licenses expire on November 30th of odd numbered years.  Thirty PDHs are required for each renewal period, and no PDHs may be carried over from the previous period.
* *Illinois SE* – Licenses expire on November 30th of even numbered years. Thirty PDHs are required for each renewal period, and no PDHs may be carried over from the previous period. A Maximum of 10 PDHs may be claimed for self-administered courses per renewal period. A Maximum of 10 PDHs may be claimed for in-house per renewal period. A Maximum of 10 PDHs may be claimed for committee memberships.
* *Florida PE* – Licenses expire on February 28th of odd numbered years. Eighteen PDHs are required for each renewal period, and no PDHs may be carried over from the previous period. One PDH must be related to laws and rules of professional engineers, and one PDH must relate to professional ethics.

As you can see, satisfying the requirements for all four licenses is a confusing ordeal. Three of the licenses expire biennially, and one expires annually. Three of them don’t allow carryover of extra earned credits, but one does allow carryover. The required number of PDHs varies from license to license. One of the licenses mandates two extremely specific credits, and another puts a maximum on the number of credits that can be earned within a few categories. Needless to say, ensuring you’ve satisfied the renewal requirements for all of these licenses is a monumental task.

Now imagine you have 10 licenses, 15 licenses, or 20 licenses. This confusion is greatly magnified with each additional license you hold. I personally maintained an extremely complicated Excel spreadsheet tracking the renewal requirements for my 15 licenses. Each licensed professional engineer I’ve ever worked with has had a different complicated method of dealing with this problem. I realized a tool was needed to ease this confusion. This tool would solve my problem, and hopefully help others also.

## The Solution

In late 2011 I had the idea to create a web-based professional engineering license management system. This system would be built to simplify the management of multiple professional engineering licenses.  Subscribers to this site would provide information on the licenses they hold, input details on each continuing education activity they complete, and the PE license manager would do the dirty work. The service would determine which continuing education activities apply to each license, calculate the outstanding amount of continuing education required for each license prior to renewal, generate continuing education logs that can be submitted with license renewal applications, and periodically email each subscriber with the state of his or her licenses.

In short, the PE license manager would be the solution to the large, complicated spreadsheets the typical professional engineer maintains to track his or her licenses.

## Platform and Hosting Details

The minimum viable product for the professional engineering license manager was built on top of the [Joomla content management system](http://www.joomla.org). Joomla was chosen to quickly implement a secure, well-supported platform with built in subscription and user level capabilities. My goal was to quickly develop an initial version (that was more of a prototype) to determine if this is a tool that professional engineers would embrace. Joomla was extended via modules to incorporate the professional engineering license manager functionality.

Pelicensemanager.com is hosted on a [Bluehost](https://www.bluehost.com) shared Linux server, and uses Joomla version 2.5.8. This server runs PHP version 5.2.17 and MySQL version 5.5.42.

## Database Design

The development of an overall database architecture for the PE license manager was the first design decision for the website. The goal of this architecture was to achieve first normal form while limiting the total number of tables needed. I settled on the following five tables:

1. *users* – Information specific to each individual user. This includes the user’s name, username, email address, etc.
2. *jurisdictions* – Information specific to each licensing jurisdiction. This includes address, phone number, website address, various continuing education requirements for the jurisdiction, etc.
3. *licenses* – Information specific to each license held by users. This includes the user id associated with the license, the jurisdiction id associated with the license, the license number, license date, etc.
4. *activities* – Information specific to continuing education activities completed by users. This includes the user id associated with the activity, date of the activity, description, awarded professional development hours, etc.
5. *conversions* – Information detailing the conversion of activity types to awarded professional development hours for specific jurisdictions. For example, the number of professional development hours awarded for each hour of teaching a seminar various from jurisdiction to jurisdiction. This table includes the associated jurisdiction id, PDHs for each continuing education credit, PDHs for each hour of teaching a seminar, etc.

The ER diagram for the implemented database is as follows:

<figure style="text-align: center">
  <img src="{{ site.url }}/images/pelicense/ER_Diagram.png" alt="">
</figure>

Being my first attempt at designing a relation database, I made several mistakes. First, and foremost, I used a horrible naming convention (which is not shown in the above diagram). In all reality, I used no real naming convention at all. The table and attribute names I originally chose were not descriptive enough in some cases, and too long and descriptive in other cases.  I varied between camel casing, all lower cases with underscores separating words, and all lower case without underscores. Quite frankly, it’s ugly.

Second, I created a separate primary key for each table, using an auto incremented integer. This makes sense for the users, activities, and jurisdictions tables, but is unnecessary for the licenses and conversions tables. The primary key for the licenses table could simply be the combination of the user_id and the jurisdiction_id. As for the conversions table, this is really a weak entity that completely depends on the jurisdictions table. Each jurisdiction is associated with one and only one entity of the conversions table. Hence, the jurisdiction_id foreign key should also function as the primary key for the conversions table.

Third, I did not enforce foreign key restrictions within the database. The use of foreign keys to associate tables through relationships is obvious from the ER diagram, but there are no imposed restrictions enforcing these foreign keys within the database itself. These restrictions are created within the code only, which could easily lead to uncaught mistakes.

If I were to redesign the database, the ER diagram would look as follows:

<figure style="text-align: center">
  <img src="{{ site.url }}/images/pelicense/Proposed_ER_Diagram.png" alt="">
</figure>

Another change that should have been included was splitting up the jurisdictions table. Though it’s not apparent in the above diagrams, the attribute list for this table is extensive. It should have been separated into several tables.

Finally, the most egregious error occurred within two attributes of the jurisdictions table. Each jurisdiction varies on the initial continuing education requirements for a licensee prior to his or her first license renewal. These requirements also differ depending on whether the initial license was obtained via exam or comity. For the initial_exam_requirement, and initial_comity_requirement attributes, I simply provided a single digit number that correlated to a requirement. I then deciphered this number in code. In retrospect, I should have created additional tables for these requirements to limit any mistakes that could be introduced in the code.

## MySQL Queries:

Another area that exposed my inexperience was the MySQL query methodology. When I implemented this web application, I had no query language experience. I chose to basically grab everything with my queries, and deciphered the results via complicated PHP algorithms. Looking back on it, this inefficient approach makes me cringe. Not only did it lead to dealing with large amounts of data in PHP, but it also made the PHP virtually unreadable.

For example, when determining the number of continuing education credits satisfied for a specific user’s license, attributes from four separate tables are required. Currently, the PE license manager grabs all attributes from all four tables before compiling the necessary information via PHP. The following four queries are used within the same algorithm:

{% highlight MySQL %}
1. SELECT *
   FROM `jurisdictions`
   WHERE `jurisdiction_id` = 'some_jurisdiction_id'
2. SELECT *
   FROM `activities`
   WHERE `user_id` = 'some_user_id'
3. SELECT *
   FROM `licenses`
   WHERE `user_id` = 'some_user_id'
   AND `jurisdiction_id` = 'some_jurisdiction_id'
4. SELECT *
   FROM `conversions`
   WHERE `jurisdiction_id` = 'some_jurisdiction_id'
{% endhighlight %}

This is horribly inefficient. A smarter query should have been used to return only the sought after information, thereby limiting the amount of code necessary to perform the calculation. For example, the following two queries should have been used instead of the previous four queries:

{% highlight MySQL %}
1. SELECT the_specificly_used_attributes
   FROM `licenses`
   INNER JOIN `conversions`
   ON licenses.jurisdiction_id = conversions.jurisdiction_id
   INNER JOIN `jurisdictions`
   ON licenses.jurisdiction_id = conversions.jurisdiction_id
   WHERE licenses.user_id = 'some_user_id'
   AND licenses.jurisdiction_id = 'some_jurisdiction_id'
2. SELECT *
   FROM `activities`
   WHERE `preapproval`
   LIKE (
     SELECT CONCAT('%', state_abbreviation, '%')
     FROM `jurisdictions`
     WHERE `jurisdiction_id` = 'some_jurisdiction_id'
   )
{% endhighlight %}

Instead of returning all values from the jurisdictions, licenses, and conversions tables separately for a given user_id and jurisdiction_id, the first query joins the three tables and returns only those attributes needed for the calculation. The second query takes advantage of the preapproval attribute of the activities table that maintains a string of jurisdictions for which the activity is approved. Instead of returning all activities, the second query limits the returned activities to only those that apply to a specific jurisdiction. These two queries take advantage of the relative speed of MySQL queries as compared to PHP code. They take the complication out of the code, and transfer it to the queries greatly improving overall efficiency and readability.

This is just one example of the inefficiencies employed in the original design of this application, but there are many others. Again, these changes have not been made due to the lack of interest in this service. Even though it is inefficient, the application works as-is for the current user base.

## Code Implementation

As previously mentioned, the application was built on top of the Joomla content management system. Choosing this platform allowed me to quickly develop a minimum viable product that I could use to gauge interest. The specific functionality was built using a series of Joomla modules. In retrospect, this methodology led to many code redundancies. A full MVC component should have been used to eliminate these redundancies.

The custom modules specific to the PE License Manager functionality are as follows:

1. *mod_ce_log* – This module allows the user to add, edit, copy, and delete individual continuing education activities. It also allows the user to view a summary of all completed continuing education activities as well as details of individual activities.
2. *mod_jurisdiction_ce_log* – This module allows the user to generate and view continuing education logs for individual licenses that user holds. It calculates the amount of applicable completed continuing education for the license, and warns the user of any outstanding requirements that must be completed prior to the next renewal.
3. *mod_jurisdictions* – This is an administrative module that facilitates the modification of jurisdictional information. The administrator can add, delete, and edit all jurisdictional information with this module.
4. *mod_jurisdiction_view* – This module allows the user to view an overall jurisdictional information summary, as well as individual detailed jurisdictional information .
5. *mod_license_overview* – This module provides an overall snapshot of the state of the user’s licenses. This snapshot includes upcoming expiration dates, completed continuing education requirements per license, and outstanding continuing education requirements per license.
6. *mod_licenses* – This module allows the user to add, edit, and delete licenses. The user can also view individual license details with this module.

As can be seen from the provided descriptions, many of these modules provide similar functionality leading to redundant code. Using a MVC component instead of individual modules would have solved this redundancy issue.

## Other features

*	The look and feel was created with a custom Joomla template.
*	There are three user levels providing specific content to that user:
  1. Guest – any non-registered user. This user has access to information about the PE License Manager.
  2. Registered – this user has full access to all tools provided by the PE License Manager.
  3. RegisteredFree – This level applies to those with an expired subscription. This user still has access to old license information and continuing education logs, but can no longer add, delete, or edit this information.
*	Monthly emails depicting the state of user licenses are sent to each subscribed user. This is currently done with a Cron job and a PHP script. Should the user base grow, a better method would be used.
*	The database is backed up daily via a Cron job and PHP script.
*	The website files are backed up weekly via a Cron job and PHP script.

## Planned features

The first planned feature is to incorporate another user level that allows that user to serve as an administrator for several engineers. This would allow that user to directly manage the licenses and continuing education activities of several engineers without needing to log into each account separately. The idea for this feature came from an inquiry that resulted from the direct mailing campaign.

The second planned feature is to expose the site functionality via a RESTful web service. A web service could facilitate the third party development of many useful features. Some examples include native mobile applications, native desktop applications, partnering with continuing education providers to automate the addition of completed activities, or partnering with jurisdictions to ensure up-to-date information.

Due to lack of overall interest in the site, these features will likely never be developed.

## Marketing Strategy

As stated in the CivilPE.net site description, organic search is not a good source of traffic for this service, so another means of marketing had to be found. CivilPE.net was created for this purpose. That site was developed to attract a targeted audience that could likely benefit from the PE License Manager. Currently, that site provides the greatest source of traffic.

When the site initially went live I did tested a targeted direct mail campaign. Each jurisdiction maintains a freely available list of licensed professional engineers, including addresses for each. I compiled several of these lists, and developed a summary of individuals licensed in three or more states. I felt that those with multiple licenses would be the most likely to use this service. I developed a postcard, and sent it to the first 100 people on that list to test the feasibility of a direct mailing campaign.

<figure class="half" style="text-align: center;">
	<img src="{{ site.url }}/images/pelicense/postcard_front.jpg" alt="">
	<img src="{{ site.url }}/images/pelicense/postcard_back.jpg" alt="">
	<figcaption>Front and Back Images of the Postcard.</figcaption>
</figure>

That campaign resulted in a few site visits and inquiries, but no subscriptions. Needless to say, I did not continue with the direct mail campaign.

## Conclusion

Developing this site was an incredible learning experience. This project was my first real exposure to PHP and MySQL. Additionally, this was the first time I really dug into using Joomla. This site was developed before I completed any formal education in computer science, and the implementation shows my lack of experience. That being said, the application worked as intended and was available to the public for nearly 6 years before the site was taken down.  As ugly as the implementation was, I’m extremely proud of the final product. Completing this project solved a personal license management problem that I grappled with for years.
Furthermore, this project finalized my decision to go back to school for a M.S. in computer science. That in and of itself was worth the time I spent developing pelicensemanager.com.
