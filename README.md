# Junior-Assessment-Project
# TKinter is a GUI library built into Python
from tkinter import *
import tkinter as tk

# All code must run inside of the Tkinter class
main = Tk()

# Window size
main.geometry("700x650")
# Did not want to resize as using absolute values for design
main.resizable(False, False)
# Title of actual window
main.title("Sabre Insurance Vehicle Catalog")
# Title Label and design elements
title = Label(main, text='Sabre Insurance Vehicle Catalog')
backgroundcolor = "#27343F"
textcolor = "#FDB713"
title.config(font=22, bg=backgroundcolor, fg=textcolor)
title.place(x=0, y=0,width=400, height=200)

data_Set = [
    {"Make": "Toyota", "Model": "Corolla", "Year": 2018, "Colour": "Red"},  
    {"Make": "Ford", "Model": "Mustang", "Year": 2019, "Colour": "Blue"},
    {"Make": "Honda", "Model": "Civic", "Year": 2020, "Colour": "Black"},
    {"Make": "Chevrolet", "Model": "Malibu", "Year": 2017, "Colour": "White"},
    {"Make": "BMW", "Model": "X5", "Year": 2021, "Colour": "Silver"},
    {"Make": "Tesla", "Model": "Model 3", "Year": 2022, "Colour": "Gray"},
    {"Make": "Hyundai", "Model": "Elantra", "Year": 2019, "Colour": "Blue"},
    {"Make": "Nissan", "Model": "Altima", "Year": 2018, "Colour": "Red"},  
    {"Make": "Volkswagen", "Model": "Jetta", "Year": 2020, "Colour": "Black"},
    {"Make": "Kia", "Model": "Optima", "Year": 2016, "Colour": "White"},
    {"Make": "Audi", "Model": "A4", "Year": 2021, "Colour": "Silver"},
    {"Make": "Mercedes-Benz", "Model": "C-Class", "Year": 2019, "Colour": "Gray"},
    {"Make": "Subaru", "Model": "Forester", "Year": 2018, "Colour": "Green"},
    {"Make": "Mazda", "Model": "CX-5", "Year": 2020, "Colour": "Red"},  
    {"Make": "Jeep", "Model": "Wrangler", "Year": 2021, "Colour": "Black"},
    {"Make": "Dodge", "Model": "Charger", "Year": 2019, "Colour": "Blue"},
    {"Make": "Lexus", "Model": "RX", "Year": 2017, "Colour": "White"},
    {"Make": "Volvo", "Model": "XC90", "Year": 2021, "Colour": "Silver"},
    {"Make": "Porsche", "Model": "Cayenne", "Year": 2022, "Colour": "Gray"},
    {"Make": "Acura", "Model": "TLX", "Year": 2020, "Colour": "Red"},

]

# Sorts data set into alphabetical order
data_Set = sorted(data_Set, key=lambda d: d["Make"])
# Adds all labels to a list so they can be overwritten if different choice is made
labels = []
current_data = []


# Add data to list, clear it when something else is called

# Called whenever there is more than 6 items to display
def see_more(dataset, page_counter, button):
    # Destroys any previous button made
    button.destroy()
    # Increment page counter in case called multiple times
    page_counter = page_counter + 1
    # Destroy all previous shown data
    for label in labels:
        label.destroy()
    # Finds length of data provided
    length = len(dataset)
    # DIV by 6 to find number of pages needed to disoo
    pages = length // 6
    if page_counter < pages:
        #Destroy all previous shown data
        for label in labels:
            label.destroy()
        temp1 = page_counter + 5
        temp2 = page_counter + 11
        #For i in the data indexes to be shown
        for i in range(temp1, temp2):
            #Finds key pair values and displays them
            for k, v in dataset[i].items():
                label = Label(main, text=f"{k:8}{v:5}")
                #Positioning
                label.pack(padx=(300, 0), pady=(0, 0))
                #Add labels to list to be overwritten
                labels.append(label)
            label = Label(main, text="**********")
            label.pack(padx=(300, 0), pady=(0, 0))
            labels.append(label)
        #Create new button, that provides dataset, what page we're on and the button to be destroyed to see_more()
        see_more_button = Button(main, text="See More",command=lambda: see_more(dataset, page_counter, see_more_button))
        see_more_button.place(x=600, y=600)
    #Selection as do not want button to spawn if no more pages to be shown
    elif page_counter == pages:
        for label in labels:
            label.destroy()
        for i in range(pages * 6, len(dataset)):
            for k, v in dataset[i].items():
                label = Label(main, text=f"{k:8}{v:5}")
                label.pack(padx=(300, 0), pady=(0, 0))
                labels.append(label)
            label = Label(main, text="***********")
            label.pack(padx=(300, 0), pady=(0, 0))
            labels.append(label)


def all_Vehicles_Printer():
    page_counter = 0
    #Find all data
    all_Data = [element for element in data_Set]
    for label in labels:
        label.destroy()
    #This selection is in all my functions as it determines whether we need to show multiple pages of information
    if len(all_Data) <= 6:
        for i in range(len(all_Data)):
            for k, v in all_Data[i].items():
                label = Label(main, text=f"{k:8}{v:5}")
                label.pack(padx=(300, 0), pady=(0, 0))
                labels.append(label)
            label = Label(main, text="***************")
            label.pack(padx=(300, 0), pady=(0, 0))
            labels.append(label)
    else:
        for i in range(0, 6):
            for k, v in all_Data[i].items():
                label = Label(main, text=f"{k:8}{v:5}")
                label.pack(padx=(300, 0), pady=(0, 0))
                labels.append(label)
            label = Label(main, text="***************")
            label.pack(padx=(300, 0), pady=(0, 0))
            labels.append(label)
        page_counter = 0
        see_more_button = Button(main, text="See More", command=lambda: see_more(all_Data, page_counter, see_more_button))
        see_more_button.place(x=600, y=600)


def vehicle_colour(colour):
    page_counter = 0
    for label in labels:
        label.destroy()
    vehicle_colour_Set = [element for element in data_Set if element["Colour"] == colour]
    if len(vehicle_colour_Set) <= 6:
        for i in range(len(vehicle_colour_Set)):
            for k, v in vehicle_colour_Set[i].items():
                label = Label(main, text=f"{k:8}{v:5}")
                label.pack(padx=(300, 0), pady=(0, 0))
                labels.append(label)
            label = Label(main, text="***************")
            label.pack(padx=(300, 0), pady=(0, 0))
            labels.append(label)
    else:
        for i in range(0, 6):
            for k, v in vehicle_colour_Set[i].items():
                label = Label(main, text=f"{k:8}{v:5}")
                label.pack(padx=(300, 0), pady=(0, 0))
                labels.append(label)
            label = Label(main, text="***************")
            label.pack(padx=(300, 0), pady=(0, 0))
            labels.append(label)
        page_counter = 0
        see_more_button = Button(main, text="See More",command=lambda: see_more(vehicle_colour_Set, page_counter, see_more_button))
        see_more_button.place(x=600, y=600)


def retrieve_vehicle_colour():
    #Retrieves colour from entry box
    colour = vehicle_colour_entered.get()
    #Capitalizes first letter of each word in order to get pass incorrect format of input
    colour = colour.capitalize()
    vehicle_colour(colour)


def vehicle_year(year):
    page_counter = 0
    for label in labels:
        label.destroy()
    vehicle_Year_Set = [element for element in data_Set if element["Year"] == year]
    if len(vehicle_Year_Set) <= 6:
        for i in range(len(vehicle_Year_Set)):
            for k, v in vehicle_Year_Set[i].items():
                label = Label(main, text=f"{k:8}{v:5}")
                label.pack(padx=(300, 0), pady=(0, 0))
                labels.append(label)
            label = Label(main, text="***************")
            label.pack(padx=(300, 0), pady=(0, 0))
            labels.append(label)
    else:
        for i in range(0, 6):
            for k, v in vehicle_Year_Set[i].items():
                label = Label(main, text=f"{k:8}{v:5}")
                label.pack(padx=(300, 0), pady=(0, 0))
                labels.append(label)
            label = Label(main, text="***************")
            label.pack(padx=(300, 0), pady=(0, 0))
            labels.append(label)
        page_counter = 0
        see_more_button = Button(main, text="See More",command=lambda: see_more(vehicle_Year_Set, page_counter, see_more_button))
        see_more_button.place(x=600, y=600)


def retrieve_vehicle_year():
    year = int(vehicle_year_entered.get())
    vehicle_year(year)


def newest_vehicles():
    page_counter = 0
    for label in labels:
        label.destroy()
    #The only thing different about this one is firstly finding what data we need to look for
    newest_Vehicles_Sort = sorted(data_Set, key=lambda d: d["Year"], reverse=True)
    search_for = newest_Vehicles_Sort[0]["Year"]
    #Then we return only that data
    newest_Vehicles_Set = [element for element in newest_Vehicles_Sort if element["Year"] == search_for]
    if len(newest_Vehicles_Set) <= 6:
        for i in range(len(newest_Vehicles_Set)):
            for k, v in newest_Vehicles_Set[i].items():
                label = Label(main, text=f"{k:8}{v:5}")
                label.pack(padx=(300, 0), pady=(0, 0))
                labels.append(label)
            label = Label(main, text="***************")
            label.pack(padx=(300, 0), pady=(0, 0))
            labels.append(label)
    else:

        for i in range(0, 6):
            for k, v in newest_Vehicles_Set[i].items():
                label = Label(main, text=f"{k:8}{v:5}")
                label.pack(padx=(300, 0), pady=(0, 0))
                labels.append(label)
            label = Label(main, text="***************")
            label.pack(padx=(300, 0), pady=(0, 0))
            labels.append(label)
        page_counter = 0
        see_more_button = Button(main, text="See More",command=lambda: see_more(newest_Vehicles_Set, page_counter, see_more_button))
        see_more_button.place(x=600, y=600)
    # Please note it did not need resorting as, when it is sorted by year, it is still in alphabetical order for that year


# Design

all_Vehicles_Button = Button(main, text="All Vehicles", command=all_Vehicles_Printer)
all_Vehicles_Button.place(x=0, y=200)
all_Vehicles_Button.config(width=56, height=2)

newest_vehicles_Button = Button(main, text="Newest Vehicles", command=newest_vehicles)
newest_vehicles_Button.place(x=0, y=250)
newest_vehicles_Button.config(width=56, height=2)

vehicle_colour_entered = tk.StringVar()
vehicle_colour_submit = Button(main, text="Enter", command=retrieve_vehicle_colour)
vehicle_colour_submit.place(x=360, y=320, width=40, height=30)
vehicle_colour_text = Label(main, text="Please enter a vehicle colour: ")
vehicle_colour_text.place(x=0, y=293)
vehicle_colour_text.config(font=16)
vehicle_Colour_Entry = Entry(main, textvariable=vehicle_colour_entered)
vehicle_Colour_Entry.place(x=0, y=320, width=360, height=30)


vehicle_year_entered = tk.StringVar()
vehicle_year_submit = Button(main, text="Enter", command=retrieve_vehicle_year)
vehicle_year_submit.place(x=360, y=390, width=40, height=30)
vehicle_year_text = Label(main, text="Please enter a year:")
vehicle_year_text.place(x=0, y=353)
vehicle_year_text.config(font=16)
vehicle_year_entry = Entry(main, textvariable=vehicle_year_entered)
vehicle_year_entry.place(x=0, y=390, width=360, height=30)

main.mainloop()
