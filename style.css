import html as html
import requests
import dash
import datetime as dt
from dash import dcc
from dash import html
import pandas as pd
import plotly.express as px

base_currency = 'NG'
yearAgo = 2.6866
key = '1442l6i0wzy2pgpxzm0sm68qkhg4o67mcu7dw4ur7t5csc2z0blrjifvnxhi'
gas = 'USD'
endpoint = 'latest'
"""
resp = requests.get(
    'https://commodities-api.com/api/' + endpoint + '?access_key=' + key + '&base=' + base_currency + '&symbols=' + gas)
if resp.status_code != 200:
    print(resp.status_code)
else:
    data = resp.json()
    print(data)"""


def today():
    today = dt.date.today()
    week_ago = today - dt.timedelta(days=7)
    return week_ago


df = pd.read_csv('test_gas_data.csv')
print(df.head())
df["Date"] = pd.to_datetime(df["Date"], format="%m/%d/%Y")
df.sort_values("Date", inplace=True)
dailyChange = str(df.iloc[0, 1] - df.iloc[1, 1])
weeklyChange = str(df.iloc[0, 1] - df.iloc[6, 1])
yearlyChange = str(df.iloc[0, 1] - yearAgo)
external_stylesheets = [
    {
        "href": "https://fonts.googleapis.com/css2?"
                "family=Lato:wght@400;700&display=swap",
        "rel": "stylesheet",
    },
]
app = dash.Dash(__name__, external_stylesheets=external_stylesheets)

app.layout = html.Div(
    html.Div(className='row', children=[
        html.Div(className='four columns div-user-controls', children=[
            html.H1('Gas Spot Prices'),
            dcc.DatePickerRange(
                id='my-date-picker-range',
                min_date_allowed=dt.date(2017, 9, 19),
                max_date_allowed=dt.date.today(),
                initial_visible_month=dt.date.today(),
                end_date=today()
            ),
        ],style={'color': '#1E1E1E'}),  # Define the left element
        html.Div(className='eight columns div-for-charts bg-grey', children=[
            dcc.Graph(
                id='Gas Spot Prices',
                config={'displayModeBar': False},
                animate=True,
                figure=px.line(df,
                               x='Date',
                               y='Close/Last',
                               template='plotly_dark').update_layout({
                    'plot_bgcolor': 'rgba(0, 0, 0, 0)',
                    'paper_bgcolor': 'rgba(0, 0, 0, 0)'})
            )]
                 )
    ])
)
if __name__ == "__main__":
    app.run_server(debug=True)
