bank - a challenge nobody solved in RC3CTF 2017, risen from the grave.  
This was a race condition challenge that had a few steps:  
1. Find and create the correct schema for the database. You can do this by using strings and seeing what gets created. The only tricky part here is the autoincrementing ID column for users.  
2. Sign up and register an account by doing a proof of work. The PoW challenge gave you the last 6 characters of a hex encoded SHA1 hash generated from random data. You needed to provide input that would generate a hash ending in those last 6 characters. The PoW was added to prevent people from just making a few thousand accounts and then transferring all of the money to one account.  
3. Take advantage of a race condition in the transfer code to get negative money (mega positive money). The function BankDatabase::completeTransaction gets the two users twice. Once before the current balance is checked against the transaction amount and once after. If you can complete a transaction multiple times in that window you can get negative money!  