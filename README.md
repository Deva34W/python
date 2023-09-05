import json

# Initialize an empty list to store job applications
job_applications = []

# Function to add a new job application
def add_job_application():
    name = input("Enter the company name: ")
    position = input("Enter the position applied for: ")
    date_applied = input("Enter the application date (YYYY-MM-DD): ")

    application = {
        "Company Name": name,
        "Position Applied For": position,
        "Application Date": date_applied
    }

    job_applications.append(application)
    print("Job application added successfully!")

# Function to view all job applications
def view_job_applications():
    if not job_applications:
        print("No job applications found.")
    else:
        for idx, application in enumerate(job_applications, 1):
            print(f"Application #{idx}:")
            for key, value in application.items():
                print(f"{key}: {value}")
            print()

# Function to update a job application
def update_job_application():
    view_job_applications()
    if not job_applications:
        return

    try:
        application_idx = int(input("Enter the application number to update: ")) - 1
        if 0 <= application_idx < len(job_applications):
            updated_field = input("Enter the field to update (Company Name/Position Applied For/Application Date): ")
            new_value = input(f"Enter the new {updated_field}: ")

            job_applications[application_idx][updated_field] = new_value
            print("Job application updated successfully!")
        else:
            print("Invalid application number.")
    except ValueError:
        print("Invalid input. Please enter a valid application number.")

# Main program loop
while True:
    print("\nJob Application Tracker")
    print("1. Add Job Application")
    print("2. View Job Applications")
    print("3. Update Job Application")
    print("4. Quit")
    choice = input("Enter your choice: ")

    if choice == "1":
        add_job_application()
    elif choice == "2":
        view_job_applications()
    elif choice == "3":
        update_job_application()
    elif choice == "4":
        with open("job_applications.json", "w") as file:
            json.dump(job_applications, file)
        print("Job applications saved to 'job_applications.json'.")
        break
    else:
        print("Invalid choice. Please select a valid option.")
