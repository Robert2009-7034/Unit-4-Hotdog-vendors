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

#test example: print all data to check it is in the list
for i in (hotdog_data):
    print(i)

# example: accessing the item of the firdt row
print(hotdog_data[0])
    
