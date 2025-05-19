# dbHandler
"""
handle calling and writing database information
Ira Garrett -- 2025
"""

import os
import json

class DBHandler:
    def __init__(self):

        # Define database directory and file path
        dbDir = "databases"
        database_one = os.path.join(dbDir, "db_one.db")
        database_two = os.path.join(dbDir, "db_two.db")

        # Ensure the directory exists
        os.makedirs(dbDir, exist_ok=True)

        # Check if database files exist, if not, create
        for i in [database_one, database_two]:
            if not os.path.exists(i):
                with open(i, "w") as f:
                    json.dump([], f, indent=4)
                print(f"{i} Database created")
            else:
                print(f"Database {i} already exists.")

    # push
    """
        push object data to db file (as a JSON)
        @object: object to push to db
        @dbFileToWriteTo: file to write to
        return 1 on success
    """
    def push(self, object, dbFileToWriteTo):
        previousContent = self.pull(dbFileToWriteTo)
        newContent = previousContent
        print(f"previous content of {dbFileToWriteTo}: {previousContent}")
        newContent.append(object.__dict__)
        print(f"updated content: {newContent}")

        with open(dbFileToWriteTo, "w") as db:
            json.dump(previousContent, db, indent=4)

        return 1


    # overwriteDB
    """
    overwrite the database with a new one
    Given a list of objects, write them into the database
    @ objectsArray: array of objects to write to database
    @ dbFileToWriteTo: file to write to
    return 1 on success
    """
    def overWriteDB(self, objectsArray, dbFileToWriteTo):
        print(f"overwriting {dbFileToWriteTo} database with {objectsArray}")

        # convert array of objects into an array of json-parsable dictionaries
        objects = []
        for i in objectsArray:
            print(i)
            try:
                objects.append(i.__dict__)
            except:
                objects.append(i)

        with open(dbFileToWriteTo, "w") as db:
            json.dump(objects, db, indent=4)
        print(f"database overwritten")
        return 1


    # pull
    """
        pull json data from file
        @dbToPull: file to pull from
        return json of data
    """
    def pull(self, dbToPull):
        try:
            with open(dbToPull, "r") as db:                       # open db in read mode
                dbJSON = json.load(db)                          # load db
            print("data pull from db")
            return dbJSON                                       # return db
        except FileNotFoundError:                               # if file is not found, return empty json
            print(f"alert: {dbToPull} does not exist, and we tried to pull from it")
            return []
        except Exception as e:
            print(f"Error!!! {e}")                            # if error occurs, log it
            return []

