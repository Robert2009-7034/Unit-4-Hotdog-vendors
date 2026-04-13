# Unit-4-Hotdog-vendors
My computing coursework.  

# Opening the text file with the needed information

# hotdog_data will store all records
hotdog_data = []

# Open this file safely, let me use it, and close it automatically
with open("Hotdogs.txt", "r") as file:

# Reads the file line by line
    for line in file:
    
# Splits the string into a list using commas
        items = line.strip().split(",")
# Converts the list into a dictionary with labels
        record = {
            "id": items[0],
            "vendor": items[1],
            "location": items[2]
        }

# Stores each record in hotdog_data
        hotdog_data.append(record))

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

# Linear Search (Sorted)
def linear_search_sorted(data, target_vendor):
    result = []
    for record in data:
        if record["vendor"] == target_vendor:
            result.append(record)

def bubble_sort(data):
    arr = data.copy()
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j]["vendor"] > arr[j + 1]["vendor"]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                return arr
