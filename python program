import time
import pandas as pd
import numpy as np

CITY_DATA = { 'chicago': 'chicago.csv',
              'new york city': 'new_york_city.csv',
              'washington': 'washington.csv' }

def get_filters():
    """
    Asks user to specify a city, month, and day to analyze.

    Returns:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    """
    print('Hello! Let\'s explore some US bikeshare data!')
    # TO DO: get user input for city (chicago, new york city, washington). HINT: Use a while loop to handle invalid inputs
    while True :
        city = input("Could you tell me in which of these cities you\'re interested Chicago or New York City or Washington?\n").lower()
        if city in CITY_DATA.keys():
                break
        else:
            print("Please check your choice again and write it")
           
                
                
                
    # TO DO: get user input for month (all, january, february, ... , june)
    months = ["january", "february", "march", "april", "may", "june"]
    while True:
        month = input("Enter the name of the month that you\'re interested in range from January to June or select all by writing all\n").lower()
        if month in months or month == "all":
            break
        else:
         print("please check your choice again and write it")
           
              
     
    # TO DO: get user input for day of week (all, monday, tuesday, ... sunday)
    days = ["saturday", "sunday", "monday", "tuesday", "wednesday", "thursday", "friday"]
    while True:
        day = input("Could you tell me in what day of the week you\'re interested? or enter all to select all days\n").lower()
        if day in days or day == "all":
            break
        else:
            print("Pleace check your choice again and write it")
            
        
    print('-'*40)
    return city, month, day

def show_me_more(df):
    """to show the user more data"""
    while True:
        show_data = input("Would you want to see 5 rows of our trip data? yes or no\n").lower()
        if show_data == "yes":
            start_row = 0
            print(df.iloc[start_row : start_row + 5])
            start_row += 5
        else:
            break    

def load_data(city, month, day):
    """
    Loads data for the specified city and filters by month and day if applicable.

    Args:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    Returns:
        df - Pandas DataFrame containing city data filtered by month and day
    """
    # loading csv files
    df = pd.read_csv(CITY_DATA[city])
    # converting the start time to datetime to get months and days from it
    df['Start Time'] = pd.to_datetime(df['Start Time'])
    # getting month from start_time column 
    df["month"] = df['Start Time'].dt.month
    # getting weekdays from start_time
    df['day_of_week'] = df['Start Time'].dt.day_name()
    # filter the month for the user 
    if month != "all":
        #using index of months to convert them
        months = ["january", "february", "march", "april", "may", "june"]
        month = months.index(month) + 1
        # apply the filter by month in my dataframe
        df = df[df["month"] == month]
    # filter by the day of the week if the user want this 
    if day != "all":
        df = df[df["day_of_week"] == day.title()]
    return df

        
def time_stats(df):
    """Displays statistics on the most frequent times of travel."""

    print('\nCalculating The Most Frequent Times of Travel...\n')
    start_time = time.time()

    # TO DO: display the most common month
    common_month = df["month"].mode()
    print("THE MOST COMMON MONTH IS: ", common_month)
    # TO DO: display the most common day of week
    common_day_week = df["day_of_week"].mode()
    print("THE MOST COMMON DAY IS: ", common_day_week) 
    # TO DO: display the most common start hour
    common_start_hour = df["Start Time"].dt.hour
    print("THE MOST COMMON HOUR IS : ", common_start_hour)
    
    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def station_stats(df):
    """Displays statistics on the most popular stations and trip."""

    print('\nCalculating The Most Popular Stations and Trip...\n')
    start_time = time.time()

    # TO DO: display most commonly used start station
    common_start_station = df["Start Station"].mode()[0]
    print("MOST COMMON START STATION IS: ", common_start_station)

    # TO DO: display most commonly used end station
    common_end_station = df["End Station"].mode()[0]
    print("MOST COMMON END STATION IS: ", common_end_station)

    # TO DO: display most frequent combination of start station and end station trip
    common_combination = df.groupby(["Start Station", "End Station"]).size().idxmax()
    print("MOST COMMON COMBINATION OF START STATION AND END STATION IS: ", common_combination) 
    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def trip_duration_stats(df):
    """Displays statistics on the total and average trip duration."""

    print('\nCalculating Trip Duration...\n')
    start_time = time.time()

    # TO DO: display total travel time
    total_travel_time = df["Trip Duration"].sum()
    print("TOTAL TRAVEL DURATION TIME IS: ", total_travel_time, "SECOND")
    # TO DO: display mean travel time
    mean_travel_time = df["Trip Duration"].mean
    print("MEAN TRAVEL TIME IS: ", mean_travel_time, "SECOND")
    
    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def user_stats(df):
    """Displays statistics on bikeshare users."""

    print('\nCalculating User Stats...\n')
    start_time = time.time()

    # TO DO: Display counts of user types
    print("COUNT OF USERS TYPE IS\n", df["User Type"].value_counts())

    # TO DO: Display counts of gender
    # washington has no gender column 
    if "Gender" in df.columns:
        print("NUMBER OF EACH GENDER IS:\n", df["Gender"].value_counts())

    # TO DO: Display earliest, most recent, and most common year of birth
    # Washington has no birth year column
    if "Birth Year" in df.columns:
        earliest = df["Birth Year"].min
        print("THE EARLIEST YEAR OF BIRTH IS:\n", earliest)
        most_recent = df["Birth Year"].max()
        print("THE MOST RECENT BIRTH IS:\n", most_recent)
        common_birth = df["Birth Year"].mode()[0]
        print("THE MOST COMMON YEAR OF BIRTH IS:\n", common_birth)
        
    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def main():
    while True:
        city, month, day = get_filters()
        df = load_data(city, month, day)
        
        time_stats(df)
        station_stats(df)
        trip_duration_stats(df)
        user_stats(df)
        show_me_more(df)
        restart = input('\nWould you like to restart? Enter yes or no.\n')
        if restart.lower() != 'yes':
            break


if __name__ == "__main__":
	main()
