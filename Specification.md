# EuroParty Specification

2017-03-16

Author: Arcadiy Kantor

## Overview
EuroParty is a website for fans of the Eurovision Song Contest who host parties to watch the contest and their guests.

EuroParty allows these fans to run their own vote, helping determine who would be the song contest winner if the only voters were the attendees of their own party.

## Background
The Eurovision Song Contest is one of the largest cultural events in Europe and an increasingly popular one worldwide. It has run annually since 1956 and draws a vast audience: more than 200 million viewers in 2016.

The song contest is a competition between bands or individual performers, each of whom represent their nation by entering a single song into the contest. Each song must be original and newly written for the song contest, and will be performed with live vocals (and optionally with live instruments) as part of the show. 

After all of the songs are performed, viewers and juries from each nation vote on which performers they thought were best. Ultimately, each country's votes produce a top 10, and points are assigned to the performers who are in that top 10. Viewers/juries in a given country cannot vote for their own country.

The voting process results in a single winner, with that performer's home nation becoming the host of the next song contest.

## System overview
In order for EuroParty to perform its role of supporting Eurovision parties, the system must incorporate some rudimentary basic data.

In particular, **parties** are associated with **events**, and the system must support multiple such events happening over time.

### Events
An event is a Eurovision Song Contest competition, which may be a final, a semi-final or even a national selection contest. 

An event consists of the following details:

- The name of the event
- The start date on which parties may be created
- The actual date of the event
- The end date on which parties may be created
- Whether this event is the current default for new parties
- A list of participants, with each participant containing:
  - The country
  - The performer's name
  - The song name
  - The performer's position in the order in which songs will be performed

### Parties
A party is a specific individual party, created by a **party host** and with **party attendees** as participants. It is associated with an event: An event may have any number of parties associated with it, but a party can only be associated to a single event.

A party consists of the following details:

- The event with which the party is associated
- The name of the party
- Information about the **party host**
- Details on the party voting rules
- A unique URL via which the party may be accessed
- An optional passphrase to vote in the party
- The results of the votes from participants at that party


## User roles
The EuroParty site has two key user roles:

1. Party host
2. Party attendee

### Party host
The party host is the individual who creates a party in the EuroParty system, determines how it will work, and disseminates the information about the party to attendees. In many cases this person will also be the host of an associated real-life party. 

Because they must manage the party in the system, the party host needs to register for an account in order to use the EuroParty site. That means that a party host can:

- Sign up for an account
- Sign in and out
- Verify their email address
- Do other administrative tasks
  - Change their password
  - Delete their account

Once the party host has an account and is signed in, the host may:
- Create a new party
- Read parties they have created
  - And in particular, view results
- Update settings for parties they have created
- Delete an existing party they have created

The party host may also be a party attendee for either their own or other parties. They don't have any special privileges as a party attendee except one: the system may store the parties they participate in and allow them to view those parties.

### Party attendee
A party attendee is a person who has been invited to participate in the party by submitting a vote for their preferred performer(s). This person need not have an account with the EuroParty site. 

A party attendee may:
- Submit a vote for their preferred performer(s)
- View the results of the party, if the party host has allowed it
- Provide their email address to get notified about the results, if the party host has allowed it


## Details
The EuroParty site will support a number of flows in order to achieve the operations and capabilities described above.

### Event management
These tasks are performed by site administrators and may or may not have a friendly interface. As a starting point these operations may be performed using scaffolding or direct database operations.

#### Adding a new event to the system
When a new event is approaching, an administrator must create this event in the EuroParty system before parties can be created for that event.

The contents of the event are described above.

#### Ending an event
In case of an issue or emergency, the administrator must be able to conclude an event before the preset end date. A concluded event may not have new parties created.

### User management
When users interact with the site, they must be able to perform certain operations related to their accounts.

#### Registration
A user must be able to create a new account in order to become a party host.

*//TODO: Account creation flowchart*

To create an account, the system must collect:
- The user's name
- The user's email address
- A password (and confirmation) for the user

*FUTURE*: Once the user creates an account, the system must validate that user's email address. It can do so by sending the user an email with a unique link the user must click. Once clicked, the user account will be fully enabled. The user may not create parties until they have validated their email address.

#### Sign in
The user must be able to sign in by entering their email address and password.

*//TODO: Sign in flowchart*

Once the user signs in they should be taken to the user main page.

*FUTURE: The user must be able to reset their password if they no longer remember it.*

#### Sign out
The user must be able to sign out of their account by clicking a sign out link.

Once the user signs out they should be taken to the home page.

#### Validate email address

*FUTURE*

#### Change password
The user must be able to change their password.

The user main page should include a link to change a user's password. They should enter their old password and their new password (twice), then the password should be updated.

### User main page
The user main page is a single special page: the user's control panel and the first place a party host will see once they sign in.

The page serves as the list of parties a party host has created and any parties they've voted in, as well as the entry point for creating new ones. It's also the entry point for any of a user's account management actions.

The page consists of the following sections:
- "New party" button: a large call to action at the top of the page to create a party.
- My parties: a list of the parties the user has created
- Parties I've voted in: a list of other user's parties this host has participated in as an attendee. Useful for viewing the results from those parties.
- Account actions: Links to sign out and change password.

*//TODO: Mockup of the user main page*

### Party
The party pages allow a host or attendee to interact with a specific party (including creating a new one). Only the voting and viewing results pages can be accessed by party attendees; all other pages may only be accessed by the party host.

#### Party creation
When a party host clicks the "new party" button, they are taken to the party creation page.

The **creation page** requires the following information:
- Event: The event the party is associated with. A dropdown with the current default event automatically selected.
- Party name: A user-visible name for the party. This is what attendees will see when they visit the party voting page.
- Voting style: The way the party host would like attendees to vote at the party. See voting styles section below.
- Party passphrase (optional): a pass phrase that party attendees will be required to enter in order to view party details and vote.

If the user cancels the party creation they will be returned to their user main page.

If the user completes the party creation, they will be taken to the party management page and shown a confirmation message.

**TEXT** (party created): "Your party is ready!"

*//TODO: Mockup of the party creation page*

##### Voting methods
Eurovision voting in real life is a complicated process that produces multiple scores from each country and then tallies the results. For the purposes of an at-home party, we want to have a simpler approach (or a variety of approaches).

The Europarty site will allow attendees to vote in one of three ways:
1. Top three (default): Voters pick their top three performers. They will be assigned 12, 10 and 8 points respectively, as per Eurovision standards.
2. Winner only: Voters can only pick their overall favorite. Each vote is assigned one point.
3. Top ten: Voters can pick their entire top ten, with points being assigned per Eurovision standards: 7-1 points for positions 4-9, then 12, 10 and 8 points for 1-3 as in the top three voting style.

The party host will be able to choose which voting method is in effect for their party.

*FUTURE*: Once the first vote is submitted, the voting method should be locked.

#### Party management
The party management page allows the party host to modify party settings as well as to view the URL 

All of the settings that were configured in the party creation page *except the event the party is associated with* should be changeable on this page.

In addition, the page should display a shareable URL to the voting page that the party host can disseminate to their party attendees.

It should also have entry points to:
- The results page
- The party deletion page
- Back to the user main page

When a user changes a setting, they should have the ability to click an "Update" button that will save their changes and then reload the party management page.

*//TODO: Mockup of the party management page*

#### Voting

*//TODO: Flow diagram for voting*

The voting page is the primary way in which *non-hosts* interact with the EuroParty service: they come to this page from a link shared with them by the party host.

If the party host has set a passphrase for the party, the attendee will need to enter that passphrase before they can view the voting form or any party details.

Once the passphrase is entered correctly (or if it was not required), the attendee will see a voting page, which displays:
- The name of the event the party is for
- The name of the party
- The name of the party host
- A brief explanation of the voting rules in accordance with the selected voting method
- An input for the user's name
- 1, 3 or 10 dropdowns (depending on the voting method), each one populated with the full list of participants in the current event
  - Each dropdown must default to a blank value until the user selects one
- A submit button

The user must select a value for each of the dropdowns, and then click "submit."

The user **does not need to sign in** in order to submit their votes. However, if they do sign in or are already signed in, once they vote the party should be recorded in their list of parties they've voted in.

If the party host has allowed guests to view results, then after clicking submit the results page will be loaded. If not, a confirmation page will be shown. In either case the page must show a confirmation message.

**TEXT** (voting confirmation): Thanks, your vote has been counted!

**FUTURE**: Validation to ensure one vote per user. Ability to sign up to get results when they're ready.

*//TODO: Mockup of the party voting page*

#### Viewing results

The results page for a given party may be displayed only to the host or to the host and any attendees with the URL (and, optionally, the aforementioned passphrase) depending on the host's preferences.

The results page should display:
- The name of the event the party is for
- The name of the party
- The name of the party host
- A brief explanation of the voting rules in accordance with the selected voting method
- The full list of participants in the event, in the order of their point total, and their number of points
- The full list of votes recorded for the party

*//TODO: Mockup of the party results page*

#### Deleting a party
The party host should be able to delete a party if they no longer want it.

They access the delete party page from the party management page.

On this page, they must confirm they wish to delete the party and informed that the action is irreversible.

**TEXT** (deletion confirmation): Once you delete a party it's gone forever. Are you sure this party's over 

*//TODO: Mockup of the party delete page*

### Home page
//TODO

### Requirements
//TODO

### Changelog

2017-03-17: Fleshed out details sections. Added TODOs.