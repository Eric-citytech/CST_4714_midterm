# CST_4714_midterm
Using direct SQL editor from Supabase

part 1:
There is a total of three Relational tables:
  8 users
  12 tickets
  21 ticket events

Explain three integrity rules:
1) Unique : This can be enforced by the primary key where each value in the column must be unique and cannot contain any duplicates

2) Error 23502 returns the not null rule in which the column cannot contain any null value.

3) The check rule returns the Error 23514 for the closed at column in the tickets table in which it raises the error when the value entered is either a null value or the closed at time is earlier than the created at time. The check rule is to ensure that the entered data is within a specific parameter

A new column was added to the tickets table using the user table's display_name column. The column is created by using a join where the tickets.requester_id matches with users.user_id columns to map out the entiries in the column. A total of 12 entries were recorded

Part 2A:
On ticket_id 1004, the current priority level is low. The update was suppose to change the priority status to high. However because the transaction was closed with a rollback, which undos all unsaved changes, the priority level of ticket_id 1004 remains at the status of low.

Part 2B:
On this test, using ticket_id 1004, an update was called to change the priority level from low to medium. Since the transaction was closed with commit, the change was preserved and ticket_id 1004's priority level has been saved to medium.

Part 3: Blocking incident
An example of blocking was when session A (PID7310) had initiated a transaction for ticket_id 1004. During this time Session B(PID7332) had also submitted an update for ticket_id 1004. Because during this time Session B was viewing a cloned data, the update was locked and was pending for Session A's transaction to complete first. Session B's update was pushed through after Session A had closed the transaction with a rollback.
  This protects Session A's changes and prevents the possibility for others to view the incomplete data for the record while it is being editted. However, since all other actions is held back until Session A's transaction is completed, it can lead Session B's update to fail because Session A's transaction if commited would make Session B's update condition being unable to find a record.

  
