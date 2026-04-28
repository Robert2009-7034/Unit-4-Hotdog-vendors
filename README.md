# Unit-4-Hotdog-vendors
# My computing coursework.  

import time


# hotdog_data will store all records
hotdog_data = []

# Open this file safely, let me use it, and close it automatically
with open("Hotdogs.txt", "r") as file:

# Reads the file line by line
    for line in file:
    
# Splits the string into a list using commas
        items = line.strip().split(",")
        
        if len(items) == 7:

            record = {
                "id": items[0],
                "vendor": items[1],
                "year_week": items[2],
                "vegan": int(items[3]),
                "meat": int(items[4]),
                "onions": float(items[5]),
                "ketchup": float(items[6])
                }

        # Stores each record in hotdog_data
        hotdog_data.append(record)

# test example: print all data to check it is in the list
for i in (hotdog_data):
    print(i)

# example: accessing the item of the firdt row
print(hotdog_data[0])



# Creating the function for the unsorted linear search
def linear_unsorted(hotdog_data, target_vendor):

    # creates a empty list to store matching records
    result = []

    # loop through each record in the hotdog_data
    for record in hotdog_data:

        # Checks that vendor id matches the target
        if record["vendor"] == target_vendor:

            result.append(record)

    #return all matching records
    return result 



# Creating the function for the bubble sort
def bubble_sort(hotdog_data):

    # Counts the total number of items in hotdog_data and store that number in num_of_records_in_list
    num_of_records_in_list = len(hotdog_data)
    
    for i in range(num_of_records_in_list-1):

        for j in range(num_of_records_in_list-i-1):

            if hotdog_data[j]["vendor"] > hotdog_data[j+1]["vendor"]:

                hotdog_data[j], hotdog_data[j+1] = hotdog_data[j+1], hotdog_data[j]

    return hotdog_data 




def quick_sort(hotdog_data):

    if len(hotdog_data) <= 1:

        return hotdog_data

    pivot = hotdog_data[len(hotdog_data) // 2]["vendor"]

    left = [x for x in hotdog_data if x["vendor"] < pivot]

    middle = [x for x in hotdog_data if x["vendor"] == pivot]

    right = [x for x in hotdog_data if x["vendor"] > pivot]

    return quick_sort(left) + middle + quick_sort(right)



# Creating the function for the sorted linear search
def linear_sorted(hotdog_data, target_vendor):

    # creates a empty list to store matching records
    result = []

    # loop through each record in the hotdog_data
    for record in hotdog_data:
        
        # Checks that vendor id matches the target
        if record["vendor"] == target_vendor:
            
            result.append(record)
            
        elif record["vendor"] > target_vendor:
            
            break
        
    #return all matching records
    return result 

def binary_search(hotdog_data, target_id):
    def find_bound(first=True):
        low = 0
        high = len(hotdog_data) - 1
        result_idx = -1  # Initialize so it returns -1 if not found

        while low <= high:
            mid = (low + high) // 2
            if hotdog_data[mid]["id"] == target_id:
                result_idx = mid
                if first:
                    high = mid - 1
                else:
                    low = mid + 1
            elif hotdog_data[mid]["id"] < target_id:
                low = mid + 1
            else:
                high = mid - 1
        return result_idx

    start = find_bound(first=True)
    if start == -1:
        return []  # Return empty if ID doesn't exist

    end = find_bound(first=False)
    
    # Returns all dictionaries that matched the target_id
    return hotdog_data[start : end + 1]


        
