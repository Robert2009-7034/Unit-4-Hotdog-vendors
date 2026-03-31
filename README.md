# Unit-4-Hotdog-vendors
My computing coursework.  

# Opening the text file with the needed information
hotdog_data = []
with open("Hotdogs.txt", "r") as file:
    for line in file:
        # .strip() removes the newline character at the end of the line and .split() breaks the string into a list based commas
        items = line.strip().split(",")

        # add the resulting list to our main list
        hotdog_data.append(items)

# test example: print all data to check it is in the list
for i in (hotdog_data):
    print(i)

# example: accessing the item of the firdt row
print(hotdog_data[0])

# creating the function for the unsorted linear search
def linear_search_unsorted(hotdog_data, target_vendor):
    # creates a empty list to store matching records
    result = []
    # loop through each record in the hotdog_data
    for record in hotdog_data:
        # Checks that vendor id matches the target
        if record["vendor"] == target_vendor:
            result.append(record)
    #return all matching records
    return result
