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
- The date of the event
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


### Details

- Event management
  - Adding a new event to the system
  - Ending an event

- User management
  - Registration
  - Sign in
  - Sign out
  - Validate email address
  - Change/reset password

- Party
  - Creation
  - Management
  - Voting
  - Viewing results
  - Deletion


### Requirements

### Future improvements