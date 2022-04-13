# README PROJECT 1 - OOP

# VELEA FLORIAN 

# GROUP 324CDb

-------------------------------------------------------------------------------

# LIBRARIES

For JSON:

    json.simple.JSONArray
    json.simple.JSONObject

For Files (writing and reading):

    java.io.FileWriter
    java.io.File
    java.io.IOException

For constructing arrays and lists:

    java.util.ArrayList
    java.util.Collections (for sorting)
    java.util.List

-------------------------------------------------------------------------------

# DESIGN PATTERNS (PACKAGE - "designpatterns.factory")

FACTORY - I've used this pattern for 2 situations:

    AgeCategoryFactory: (To place the child in his coresponding category)
        Each child needs to be placed in a age category for us to apply the
        right strategy for us to calculate exactly the budget for every child
    
        CATEGORIES:
            BABY - 5< YEARS
            KID - 5 - 12 YEARS (but lower than 12)
            TEEN - 12 - 18 YEARS (but lower than 18)
            ADULT - >18 YEARS

    AverageScoreFactory: (Creates a strategy by a based on the child's age
                            category)
        Now that every child has been placed into a category, we can apply
        a strategy to calculate the budget. This factory creates that stra-
        tegy.

STRATEGY:

    AverageScoreStrategy: (Interface that will be implemented by other strategies)
        contains one method - getAverageScore().

        STRATEGIES:
            These strategies not only calculate the average score, but also add
            to the history of nice scores of the given child the new value.
            
            BabyStrategy: 
                Makes the average score 10.

            KidStrategy:
                Based on the given formula (arithmetic mean) we calculate the
                the averageScore, with the niceScoreHistory of each child
            
            TeenStrategy:
                Based on the given formula (weighted average) we calculate the
                the averageScore, with the niceScoreHistory of each child

-------------------------------------------------------------------------------

# ENUMS (PACKAGE - "enums")

    I think they came with the skel of the project. Didn't modify them at all

-------------------------------------------------------------------------------

# COMMON (PACKAGE - "common")

    Contains constants that prevent using 'Magic numbers', making the code
    easier to understand.

-------------------------------------------------------------------------------

# READER INPUT AND WRITER (PACKAGE - "fileio")

    READ:

        When we read from the Json file we need to stock the information as it's 
        given in the file, so I created some classes to help me read and 
        modify this data.

        INPUT:
            Implemented with a few classes, like:
                
                'InputLoader' - Converts the data from the json file to 
                exactly what we need for this project. Utilieses a JsonParser
                to read the file and based on the type of data we need,
                it converts to it (for example, from the file we need the 
                children that will pe on Santa's list, so we read this information
                and converts the data to a java ArrayList)

                'Input' - Will contain the information given in the Json File.
                This input will be divided in multiple classes like:
                    
                    "ChildrenInputData" - contains the data for the children from
                    round 0.

                    "SantaGiftsInputData" - contains the data for the gifts Santa
                    has in the first round.

                    "AnnualChangesInputData" - contains all the data from annual
                    changes, beside the data for the children updates.

                    "ChildrenUpdateInputData" - contains all the updates for
                    children from all annual changes.
                
                'ShowInput' - Class that has methods to show the data. 
                (makes debugging easier)

                'BudgetCalculator' - calculates the budget for every child based
                on it's average score. (This one is for the completion of the data)

    WRITE:

        'Writer':
            For writing the output I used one class that will take the data from 
            Santa's list (contains all the data about the children - age, budget, what
            gifts they receive etc.) and creates the json. Also contains a method that
            closes the file.

-------------------------------------------------------------------------------

# Children (PACKAGE - "children")

    Contains all methods to construct and modify data from input for the children.

        Child - Class that will contain all the data, including the the age category
        of the child, nice score history and the recievied gifts. On this data we will
        work.

        AnnualAgeRevision - Contains methods to increment the age of the children,
        to check if they are over 18 years old and recalculate the strategy for the
        child (if need it).

        UpdateChildrenData - Class that updates the data for the children on Santa's
        list. Firstly, it updates the the average score of the child and adds to
        the nice score list, then updates the gift preferences.

-------------------------------------------------------------------------------

# Gifts (Package - "gifts")

    Contains all the data of Santa's gifts and a class that let's us add new gifts
    to the children gifts list of the current year.

-------------------------------------------------------------------------------

# main (Package - "main")

    This is where all the magic happens. We could consider this as the simulation
    of the project, where all the classes are combined to give us the wanted output.

# Flow of project

    The flow starts in main, where I firstly read and convert the input from the
    json tests (using classes from #input). After I convert the information, I
    distribute it to the corespoding objects (example, the information about the
    children I place it on the list of children, data about the gifts I place it
    on etc.).
    The first round starts. Firstly, the objective is to check and place every
    child in an age category (here we use the factory and strategy pattern I mention
    earlier) and we immediately follow up with the budget calculation for every child.
    Next step is to assign the gifts to the children by their preferences and budget.
    For an easier search, I sorted the gift list from lowest price to highest, so I can
    give the child the first gift that coresponds with it's preference.
    Now annual changes start to happen. We start by incrementing the ages of the
    the current children, if there any changes need it to be done (maybe they change
    age categories, so we have to change the strategy for them), we add the new
    children (if there are any to be add), and then we update the children's info
    (if there is any to be updated). After this, the next steps are exactly like 
    the first round. We write all this on the output file using a JsonWriter.
     
# Santa-s-database
