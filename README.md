# carbon-tracker

Creating a Python tool called "carbon-tracker" involves developing a simple program that collects data about various digital activities, calculates a carbon footprint estimate, and provides suggestions for reducing it. For this example, we’ll simulate digital activity data and incorporate basic carbon footprint calculations. The program will include comments and error handling for educational purposes.

Here is a simple implementation:

```python
import logging

# Set up basic logging configuration to output debug information
logging.basicConfig(level=logging.DEBUG, format='%(asctime)s - %(levelname)s - %(message)s')

class CarbonTracker:
    def __init__(self):
        """Initialize tracker with digital activities and their respective carbon emission factors."""
        self.activities = {
            "emails_sent": 4,  # grams of CO2e per email
            "google_searches": 0.2,  # grams of CO2e per search
            "video_streaming_hours": 200,  # grams of CO2e per hour
            "video_calls_hours": 50  # grams of CO2e per hour
        }
        self.activity_data = {}

    def collect_data(self):
        """Prompt user to enter data for each digital activity."""
        for activity in self.activities:
            while True:
                try:
                    data = input(f"Enter the number of {activity} in the last month: ")
                    self.activity_data[activity] = float(data)
                    logging.info(f"Collected data for {activity}: {self.activity_data[activity]}")
                    break
                except ValueError:
                    logging.error("Invalid input. Please enter a number.")
                    print("Please enter a valid number.")

    def calculate_footprint(self):
        """Calculate the total carbon footprint based on collected data."""
        total_emission = 0.0
        for activity, value in self.activity_data.items():
            emission = value * self.activities[activity]
            total_emission += emission
            logging.debug(f"Calculated {emission}g CO2e for {value} {activity}.")
        logging.info(f"Total CO2e emissions: {total_emission} grams.")
        return total_emission

    def suggest_reductions(self, total_emission):
        """Provide suggestions for reducing carbon footprint based on total emissions."""
        print("\nSuggestions for reducing your carbon footprint:")
        if total_emission > 1000:
            print("1. Reduce the number of emails sent by cleaning up your mailing list.")
            print("2. Use energy-efficient devices for streaming and video calls.")
            print("3. Lower video streaming quality to save data and energy.")
        else:
            print("You're doing a great job minimizing your carbon footprint!")
            print("Consider sharing your practices with others to make a broader impact.")

def main():
    print("Welcome to Carbon Tracker!")

    tracker = CarbonTracker()
    
    try:
        tracker.collect_data()
        total_emission = tracker.calculate_footprint()
        tracker.suggest_reductions(total_emission)
    except Exception as e:
        logging.critical(f"An unexpected error occurred: {e}")
        print(f"An unexpected error occurred. Please try again. Error: {e}")

if __name__ == "__main__":
    main()
```

### Key Features:

- **Activity Data Collection**: The program collects data for different digital activities from the user.
- **Carbon Footprint Calculation**: Using predefined emission factors for each activity, it calculates the total carbon footprint.
- **Suggestions for Reduction**: Based on the calculated emissions, the program provides tips to help users reduce their carbon footprint.
- **Error Handling**: The program includes basic input validation and error handling.

### Further Enhancements:
For a real-world application, the program could be expanded to integrate with APIs for more accurate digital activity monitoring, use databases to track history, and employ advanced algorithms to offer more personalized suggestions.