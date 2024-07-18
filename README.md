from google.colab import drive

# Mount Google Drive
drive.mount('/content/drive')

import pandas as pd

# Load the processed DataFrame from the CSV file
file_path = '/content/drive/My Drive/selected_columns_data.csv'
df = pd.read_csv(file_path)

def calculate_XRuns(inns_rr, inns_wkts, inns_balls_rem):
    try:
        # Convert inputs to float (if they are not already)
        inns_rr = float(inns_rr)
        inns_wkts = float(inns_wkts)
        inns_balls_rem = float(inns_balls_rem)

        # Look up XRuns value based on the input values
        xruns_value = df[(df['inns_rr'] == inns_rr) &
                         (df['inns_wkts'] == inns_wkts) &
                         (df['inns_balls_rem'] == inns_balls_rem)]['XRuns'].values[0]

        return xruns_value

    except IndexError:
        return "No matching data found."
    except Exception as e:
        return str(e)

# Example usage:
inns_rr_input = input("Enter inns_rr value: ")
inns_wkts_input = input("Enter inns_wkts value: ")
inns_balls_rem_input = input("Enter inns_balls_rem value: ")

xruns = calculate_XRuns(inns_rr_input, inns_wkts_input, inns_balls_rem_input)
print(f"XRuns value: {xruns}")
