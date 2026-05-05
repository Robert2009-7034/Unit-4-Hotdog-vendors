# Unit-4-Hotdog-vendors
# My computing coursework.  

# Imports the time module that will allow me to compare all the different types of searches and sorts to find the most efficient ones
import time

#  Creates a list called hotdog_data that will store all records and be used throughout my coursework
hotdog_data = []

# Open this file safely so the vendors information is available to use for the sorts and searches, let me use it, and close it automatically
with open("Hotdogs.txt", "r", encoding="utf-8") as file:

    # Reads line by line in the file so my sorts and searches can actually sort and search through the list 
    for line in file:
    
# Splits the string into a list using commas so all the information about the vendors are properly separated 
        items = line.strip().split(",")
        
        # Checks that there is the correct numberr of items in the list which is 7 as there is the id, vednor, year_week, vegan, meat, onions and ketchup
        if len(items) == 7:

            # Creates a dictionary for each record with the appropriate data types as all the different types of items have different measurements
            record = {
                "id": items[0],
                "vendor": items[1],
                "year_week": items[2],
                "vegan": int(items[3]),
                "meat": int(items[4]),
                "onions": float(items[5]),
                "ketchup": float(items[6])
                }

            # Stores each record in hotdog_data so I can use the variable hotdog_data in my searches and sorts
            hotdog_data.append(record)

# test example: print all data to check it is in the list
for i in (hotdog_data):
    print(i)

# example: accessing the item of the first row
print(hotdog_data[0])



# Creating the function for the unsorted linear search
def linear_unsorted(hotdog_data, target_vendor):

    start_time_linear_unsorted = time.perf_counter()

    # creates a empty list to store matching records
    result = []

    # loop through each record in the hotdog_data
    for record in hotdog_data:

        # Checks that vendor id matches the target
        if record["vendor"] == target_vendor:

            result.append(record)

    end_time_linear_unsorted = time.perf_counter()

    total_linear_unsorted_time = end_time_linear_unsorted - start_time_linear_unsorted

    print(f"The totle time it took the unsorted linear to be complete is: {total_linear_unsorted_time:.8f}s")

    #return all matching records
    return result 



# Creating the function for the bubble sort
def bubble_sort(hotdog_data):

    start_time_bubble_sort = time.perf_counter()

    # Counts the total number of items in hotdog_data and store that number in num_of_records_in_list
    num_of_records_in_list = len(hotdog_data)
    
    # An outer loop that controls the how many passes the inner loop will make
    for i in range(num_of_records_in_list-1):

        # An inner loop which compares and swaps adjacent items in each pass
        for j in range(num_of_records_in_list-i-1):

            # Checks if the current record's vendor is greater than the next recorded vendor
            if hotdog_data[j]["vendor"] > hotdog_data[j+1]["vendor"]:

                # Swaps the two records if the current record's vendor is greater than the next record's vendor
                hotdog_data[j], hotdog_data[j+1] = hotdog_data[j+1], hotdog_data[j]

    end_time_bubble_sort = time.perf_counter()

    total_time_bubble_sort = end_time_bubble_sort - start_time_bubble_sort

    print(f"The totle time it took the bubble sort to be complete is: {total_time_bubble_sort:.8f}s")

    # returns the sorted list of records
    return hotdog_data



# Creating the function for the quick sort
def quick_sort(hotdog_data):

    start_time_quick_sort = time.perf_counter()
    
    # Checks if the list has 0 or 1 item
    if len(hotdog_data) <= 1:

        end_time_quick_sort = time.perf_counter()

        total_time_quick_sort = end_time_quick_sort - start_time_quick_sort

        print(f"The totle time it took the bubble sort to be complete is: {total_time_quick_sort:.8f}s")

        # returns the list as it is already sorted
        return hotdog_data
        
    # Chooses a pivot value, which is used to split the list
    pivot = hotdog_data[len(hotdog_data) // 2]["vendor"]

    # Creates a list of all records where the vendor is less than the pivot value
    left = [x for x in hotdog_data if x["vendor"] < pivot]

    # Creates a list of all records where the vendor is equal to the pivot value
    middle = [x for x in hotdog_data if x["vendor"] == pivot]

    # Creates a list of all records where the vendor is greater than the pivot value
    right = [x for x in hotdog_data if x["vendor"] > pivot]

    end_time_quick_sort = time.perf_counter()

    total_time_quick_sort = end_time_quick_sort - start_time_quick_sort

    print(f"The totle time it took the bubble sort to be complete is: {total_time_quick_sort:.8f}s")

    #  Sorts the left and right lists and combines them with the middle list a sorted list of records
    return quick_sort(left) + middle + quick_sort(right)



# Creating the function for the sorted linear search
def linear_sorted(hotdog_data, target_vendor):

    start_time_linear_sorted = time.perf_counter()

    # creates a empty list to store matching records
    result = []

    # loop through each record in the hotdog_data
    for record in hotdog_data:
        
        # Checks that vendor id matches the target
        if record["vendor"] == target_vendor:
            
            # Adds the dicionary called record
            result.append(record)
        
        # Checks that vendor id matches the target
        elif record["vendor"] > target_vendor:
            
            break

    end_time_linear_sorted = time.perf_counter()

    total_linear_sorted_time = end_time_linear_sorted - start_time_linear_sorted 

    print(f"The totle time it took the sorted linear to be complete is: {total_linear_sorted_time:.8f}s")

    #return all matching records
    return result 

# A function to search for records with a specific id using a binary search
def binary_search(hotdog_data, target_id):
    
    start_time_binary_search = time.perf_counter()   
    
    # A helper function to find either the first or last occurrence of the target id
    def find_bound(first=True):
        
        # Sets the starting index of the search range
        low = 0
        
        # Sets the ending index of the search range
        high = len(hotdog_data) - 1
        
        # Stores the index of a found match but stays at -1 if no match is found
        result_index = -1  
        
        # Runs the binary search loop while there is still a valid search range
        while low <= high:
            
            # Calculates the middle index of the current search range
            mid = (low + high) // 2
            
            # Checks the middle element matches the target ID
            if hotdog_data[mid]["id"] == target_id:
                
                # Stores the index where the match was found
                result_index = mid
                
                # If searching for the first occurrence continue searching to the left
                if first:
                    
                    # Moves the search range to the left half
                    high = mid - 1
                    
                # If searching for the last occurrence continue searching to the right
                else:
                    # Moves the search range to the right half
                    low = mid + 1
                
            # If the middle ID is smaller than the target search the right half         
            elif hotdog_data[mid]["id"] < target_id:
                
                # Narrows the search by updating the lower bound
                low = mid + 1
                
            else:
                
                # Narrows the search by updating the upper bound
                high = mid - 1
        # returns the index of the occurrence or -1 if not found        
        return result_index
    
    # Finds the first position where the target ID appears    
    start = find_bound(first=True)

    # Checks if the target ID was not found at all
    if start == -1:

        end_time_binary_search = time.perf_counter()
        
        total_binary_search_time = end_time_binary_search - start_time_binary_search
        
        print(f"The total time it took the binary search to be complete is: {total_binary_search_time:.8f}s")
        
        # returns an empty list if no match is found
        return []  

        
    # Finds the last position where the target ID appears     
    end = find_bound(first=False)

    end_time_binary_search = time.perf_counter()

    total_binary_search_time = end_time_binary_search - start_time_binary_search

    print(f"The total time it took the binary search to be complete is: {total_binary_search_time:.8f}s")

    # Returns all dictionaries that matched the target_id
    return hotdog_data[start : end + 1]

