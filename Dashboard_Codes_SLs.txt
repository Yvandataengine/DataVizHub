#__IMPORTING NEEDED PACKAGES_____
import pandas as pd
import streamlit as st
import plotly.express as px
from PIL import Image
import openpyxl
import plotly.graph_objects as go
import time
from streamlit_option_menu import option_menu
import matplotlib.pyplot as plt
from matplotlib.patches import Circle
from matplotlib.colors import LinearSegmentedColormap


#___IMPORTING DATAFRAMES FROM EXCEL_____
#_(1)_GDP at Current prices DF___
excel_file_GDPCP = 'GDPdata.xlsx'
sheet_name = 'CYGDP CP'
df_GDPCP = pd.read_excel(excel_file_GDPCP,
                   sheet_name=sheet_name,
                   usecols='D:AD',
                   header=4)
#___Dropping unnecessary rows & columns___
rows_to_drop_GDPCP = [0, 39, 41, 42, 43]
df_GDPCP = df_GDPCP.drop(rows_to_drop_GDPCP)

column_to_drop_GDPCP = 'Unnamed: 5'
df_GDPCP = df_GDPCP.drop(column_to_drop_GDPCP, axis=1)

#_(2)_GDP at constant 2017 prices
excel_file_GDPKP = 'GDPdata.xlsx'
sheet_name = 'CYGDP KP'
df_kp = pd.read_excel(excel_file_GDPKP,
                   sheet_name=sheet_name,
                   usecols='D:AD',
                   header=4)
#___Dropping unnecessary rows & columns___
rows_to_drop_kp = [0, 39, 41, 42, 43]
df_kp = df_kp.drop(rows_to_drop_kp)

column_to_drop_kp = 'Unnamed: 5'
df_kp = df_kp.drop(column_to_drop_kp, axis=1)


#_(3)_GDP by Expenditure
excel_file_GDPexp = 'GDPdata.xlsx'
sheet_name = 'T3 GDP CY'
df_expenditure = pd.read_excel(excel_file_GDPexp,
                   sheet_name=sheet_name,
                   usecols='D:AD',
                   header=5)

#___Dropping unnecessary rows & columns___
rows_to_drop_GDPexp = [0,6,12,20,21,22,23,24,25,26,27,28,29,30,
                       31,32,33,34,35,36,37,38,39,40,41,42,43,44,
                       45,46,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63]
df_expenditure = df_expenditure.drop(rows_to_drop_GDPexp)

column_to_drop_GDPexp = 'Unnamed: 4'
df_expenditure = df_expenditure.drop(column_to_drop_GDPexp, axis=1)


#_(4)_CPI Rwanda, Urban & Rural
excel_file_CPIURBAN = 'CPIdata.xlsx'
sheet_name = 'Urban'
df_cpiurban = pd.read_excel(excel_file_CPIURBAN,
                   sheet_name=sheet_name,
                   usecols='D:FO',
                   header=3)

excel_file_CPIRURAL = 'CPIdata.xlsx'
sheet_name = 'Rural'
df_cpirural = pd.read_excel(excel_file_CPIRURAL,
                   sheet_name=sheet_name,
                   usecols='D:FO',
                   header=3)

excel_file_CPIRDA = 'CPIdata.xlsx'
sheet_name = 'All Rwanda'
df_cpirda = pd.read_excel(excel_file_CPIRDA,
                   sheet_name=sheet_name,
                   usecols='D:FO',
                   header=3)

#___TITLES___
st.set_page_config(page_title="Rwanda's GDP 2022,",
                   page_icon=":bar_chart:",
                   layout="centered")

#st.header("RWANDA'S 2022 GDP AND CPI")


# Centered header using custom class
st.markdown('<h2 class="centered-header">RWANDA 2022 GDP AND CPI</h2>', unsafe_allow_html=True)




   #___OPTION-MENU


#1. as a sidebar menu
with st.sidebar:
    selected = option_menu(
        menu_title="Main Menu",
        options=["Home", "Data", "More statistics"],
        icons=["house", "folder", "plus-lg"],
        menu_icon="cast",
        default_index=0,
        orientation="vertical",
        styles={
            "container": {"padding": "0!important", "background-color": "rgba(46, 87, 138, 0.2)"},
            "icon": {"color": "auto", "font-size": "20px"},
            "nav-link": {
                "font-size": "25px",
                "text-align": "left",
                "margin": "0px",
                "--hover-color": "rgba(46, 87, 138, 0.15)",
            },
            "nav-link-selected": {"background-color": "rgba(46, 87, 138, 0.5)"}
        },
    )

st.sidebar.write("Designed by;")
if st.sidebar.checkbox("STATSLAB"):
    st.sidebar.caption("AYINEBYONA Prosper")
    st.sidebar.caption("HANGU Dieu Merci")
if selected == "Home":

    # space_function
    st.write('#        ')
    # __Part 2.Important Economic Indicators___


    # Custom CSS for centering the header
    custom_css_header_important_economic_indicators = """
        <style>
            .centered-header {
                text-align: center;
            }
        </style>
    """

    # Display the custom CSS
    st.markdown(custom_css_header_important_economic_indicators, unsafe_allow_html=True)

    # Centered header using custom class
    st.markdown('<h3>🔍 2022 IMPORTANT ECONOMIC INDICATORS</h3>', unsafe_allow_html=True)

    # Custom colors for component
    custom_color_1_imp = "rgba(46, 87, 138, 0.2)"  #1color code
    custom_color_2_imp = "rgba(57, 136, 128, 0.2)"  #2color code
    custom_color_3_imp = "rgba(66, 161, 191, 0.2)"  #3color code
    custom_color_4_imp = "rgba(28, 141, 197, 0.2)"  #4color code

    # Custom CSS for styling the components
    custom_css_imp = f"""
        <style>
            .custom-message-1 {{
                background-color: {custom_color_1_imp};
                color: auto;
                padding: 8px;
                border-radius: 5px;
                text-align: center;
            }}

            .custom-message-2 {{
                background-color: {custom_color_2_imp};
                color: auto;
                padding: 8px;
                border-radius: 5px;
                text-align: center;
            }}

            .custom-message-3 {{
                background-color: {custom_color_3_imp};
                color: auto;
                padding: 8px;
                border-radius: 5px;
                text-align: center;
            }}

            .custom-message-4 {{
                background-color: {custom_color_4_imp};
                color: auto;
                padding: 8px;
                border-radius: 5px;
                text-align: center;
            }}
        </style>
    """

    # Display the custom CSS
    st.markdown(custom_css_imp, unsafe_allow_html=True)

    # Custom content for info and success messages
    info_content1_imp = """
        <div class="custom-message-1">
            <div style="font-size: 16px;">Total GDP</div>
            <div style="font-size: 36px;">13,716</div>
            <div style="font-size: 14px;">Billions Rwf</div>
        </div>
    """

    success_content2_imp = """
        <div class="custom-message-2">
            <div style="font-size: 16px;">GDP per capita</div>
            <div style="font-size: 36px;">1,035</div>
            <div style="font-size: 14px;">Thousands Rwf</div>
        </div>
    """

    success_content3_imp = """
        <div class="custom-message-3">
            <div style="font-size: 16px;">Consumer Price Index</div>
            <div style="font-size: 36px;">180.9</div>
            <div style="font-size: 14px;">(80% increase from 2014)</div>
        </div>
    """

    success_content4_imp = """
        <div class="custom-message-4">
            <div style="font-size: 16px;">Total population</div>
            <div style="font-size: 36px;">13.3</div>
            <div style="font-size: 14px;">Millions</div>
        </div>
    """

    # Display custom info and success messages
    col1, col2, col3, col4 = st.columns(4)

    with col1:
        st.markdown(info_content1_imp, unsafe_allow_html=True)

    with col2:
        st.markdown(success_content2_imp, unsafe_allow_html=True)

    with col3:
        st.markdown(success_content3_imp, unsafe_allow_html=True)

    with col4:
        st.markdown(success_content4_imp, unsafe_allow_html=True)

    # __Part 3. GDP and Economic Growth___
    st.write(" ")
    st.write(" ")
    st.write(" ")


    st.markdown('<h3>📊 GDP AND ECONOMIC GROWTH</h3>', unsafe_allow_html=True)

    # ___GDP by Kind of Activity (pie chart)___
    selected_rows = df_GDPCP.iloc[[2, 8, 22, 38], [0, -1]]  # Selecting rows by index and columns by name
    # Renaming the columns for better labeling
    selected_rows.columns = ['Activities description', '2022']


    # Create a pie chart

    def ring_pie_chart(data, legend_text_color='black'):
        # Extract data from DataFrame
        labels = data['Activity description'].tolist()
        sizes = data[2022].tolist()

        # Colors for the rings
        colors = ['#398880', '#1C8DC5', '#2E578A', '#5AA136']

        # Plot the ring pie chart
        fig, ax = plt.subplots(figsize=(8, 8))  # Adjust the figure size as needed
        wedges, text, autotext = ax.pie(
            sizes,
            autopct='%1.1f%%',
            startangle=90,
            colors=colors,
            wedgeprops=dict(width=0.4, alpha=1),  # Set alpha for transparency
            labels=None,  # Use labels directly in the legend
            pctdistance=0.8,  # Adjust the distance of labels from the center
        )

        # Set the color of percentage values to white
        for autotext_label in autotext:
            autotext_label.set_color('white')
            autotext_label.set_size(18)

        # Move the legend below the pie chart and customize legend text color
        legend = ax.legend(wedges, labels, loc="upper center", bbox_to_anchor=(0.5, 0), ncol=4)

        # Remove legend box borders (strokes)
        legend.get_frame().set_linewidth(0)

        # Create a custom gradient color for the legend box
        legend.get_frame().set_facecolor('none')  # Set the background color of the legend box
        for text_item in legend.get_texts():
            text_item.set_color(legend_text_color)  # Set the color of legend text

        # Customize legend text color
        for text_item in legend.get_texts():
            text_item.set_color(legend_text_color)

        # Set the background of the entire figure to be transparent
        fig.patch.set_alpha(0.0)

        return fig


    st.write(" ##### 1. Gross Domestic product by Kind of Activity (at current prices)")
    st.caption("‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎")
    st.write("###### GDP by Kind of Activity(% contribution) in Rwf billions")


    col1, col2 = st.columns([10, 3.5])

    with col1:

        # Streamlit app

        # Assuming `selected_rows` is your DataFrame from the Excel file
        selected_rows = df_GDPCP.iloc[[2, 8, 22, 38], [0, -1]]

        # Display the ring pie chart with customizable legend text color and gradient legend box color
        fig = ring_pie_chart(selected_rows, legend_text_color='grey')
        st.pyplot(fig)

    with col2:
        #st.write("‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎")
        st.caption("Measured at 13,716 Rwf billions, Rwanda's GDP is mainly influenced by the service sector"
                   " which was measured at 6,377 Frw billions, "
                   "and the agriculture and industry sectors contributing "
                   "almost equally with 3,415 Frw billions and 2,913 Frw billions"
                   " respectively, while Adjustment for taxes less subsidies was measured at 1,012 Frw billions")

    # ___GDP by Expenditure___
    st.caption("‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎")
    st.write(" ##### 2. Gross Domestic product by Expenditure (at current prices)")

    # Select specific rows for creating bar graphs
    selected_rows_GDPexpenditure = df_expenditure.iloc[[4, 5, 3, 10], [0, -1]]

    # Rename the columns for better labeling
    selected_rows_GDPexpenditure.columns = ['Expenditure', '2022']

    # Define custom colors for each expenditure category
    custom_colors = {'Government': '#42A1BF',
                     'Gross capital formation': '#1C8DC5',
                     'Resource balance': '#398880',
                     'Households and NGOs': '#2E578A'}

    # Remove leading/trailing whitespaces from category names
    selected_rows_GDPexpenditure['Expenditure'] = selected_rows_GDPexpenditure['Expenditure'].str.strip()

    # Create a bar graph with custom colors
    figEx = px.bar(selected_rows_GDPexpenditure,
                   x='Expenditure',
                   y='2022',
                   text='2022',
                   title='2022 GDP by Expenditure',
                   color='Expenditure',
                   color_discrete_sequence=[custom_colors[exp] for exp in selected_rows_GDPexpenditure['Expenditure']],
                   category_orders={'none': list(custom_colors.keys())},
                   hover_data={'2022': True})

    # Update layout for text orientation and size
    figEx.update_layout(yaxis_title='Expenditure in Frw billions', xaxis_title='',
                        font=dict(size=17),
                        legend_title_text='Expenditure by category',
                        showlegend=False)

    # Hide x-axis labels
    figEx.update_xaxes(showticklabels=True)

    # Add x-axis title under the chart
    figEx.update_layout(xaxis=dict(title=dict(text='Expenditure by category')))

    # Show the plot
    st.plotly_chart(figEx)

    # GDP BY EXPENDITURE CHECKBOX+__________________________________________________________________________________________________________________
    # Data
    data = {
        'Type_exp_rb': ['Net Export', 'Net Import', 'Resource Balance'],
        'Amount_exp_rb': [3084, 5197, -2113]
    }

    df = pd.DataFrame(data)

    # Plot
    fig_add_resource_balance = px.bar(df, x='Type_exp_rb', y='Amount_exp_rb', text='Amount_exp_rb', color='Type_exp_rb',
                                      labels={'Amount_exp_rb': 'Amount_exp_rb'},
                                      color_discrete_map={'Net Export': '#9CC3C0', 'Net Import': '#6BA6A0',
                                                          'Resource Balance': '#398880'})

    # Update layout to adjust the size
    fig_add_resource_balance.update_layout(

        yaxis_title='Expenditure in Billions Rwf',
        xaxis_title='Expenditure by category',
        showlegend=False,
        height=300,  # Adjust the height as needed
        width=400  # Adjust the width as needed
    )

    if st.checkbox("Why a negative Resource balance?"):
        st.write("##### Rwanda's Exports and Imports in 2022")

        cola_rb, colb_rb = st.columns([10, 6])
        with cola_rb:
            # Show the plot
            st.plotly_chart(fig_add_resource_balance)

        with colb_rb:
            st.title("               ")
            st.title("               ")
            st.write("Source of negative Resource balance")
            st.caption("Due to higher imports than exports the Resource balance was negative")

    # __Economic growth__
    st.write(" ##### 3. Economic growth")

    # __intro to growth
    st.markdown(
        "The recent year has seen Economic growth, with the GDP rising by 25.5% when measured at current prices"
        " and 8.2% when measured at constant 2017 prices. The Economic growth when evaluated at constant 2017 prices, "
        "the growth rate appears comparatively lower, reflecting the adjustments made for inflationary effects. "
        "This adjustment accounts for changes in price levels, presenting a more accurate depiction of the actual increase "
        "in the quantity of goods and services produced, independent of inflation."
    )

    # __Economic growth__

    # ____Extracting the 'Item' and the data for plotting the line graphs
    item_cp = df_GDPCP.iloc[0, 0]
    x_values_cp = df_GDPCP.columns[2:].astype(int)
    y_values_cp = df_GDPCP.iloc[0, 2:].astype(float)

    item_kp = df_kp.iloc[0, 0]
    x_values_kp = df_kp.columns[2:].astype(int)
    y_values_kp = df_kp.iloc[0, 2:].astype(float)


    # ____Creating the line graph
    fig_GDPgrowthrate = go.Figure()

    # ____Adding the first line from the df_GDPcp dataframe with custom color
    fig_GDPgrowthrate.add_trace(go.Scatter(x=x_values_cp, y=y_values_cp, mode='lines', name='GDP at Current prices',
                                           line=dict(color='#5AA136')))

    # ____Adding the second line from the df_kp dataframe with custom color
    fig_GDPgrowthrate.add_trace(
        go.Scatter(x=x_values_kp, y=y_values_kp, mode='lines', name='GDP at Constant 2017 prices',
                   line=dict(color='#2E578A')))

    # ____Updating the layout
    fig_GDPgrowthrate.update_layout(title='Economic growth at different prices',
                                    xaxis_title='Year',
                                    yaxis_title='Total GDP in Frw billions')

    # __Show the line graph
    st.plotly_chart(fig_GDPgrowthrate)

    st.caption("Use the slider below to select the specific range of your choice to see its Economic growth rate")

    # __Economic growth rate slider__
    # ____Adding a slider to select the range of years
    selected_years_GDPgrowthrate = st.slider('Select Range of Years', min_value=1999, max_value=2022,
                                             value=(1999, 2022))

    # ____Finding the corresponding indices for the selected years in the first dataframe (df_cp)
    start_year_cp, end_year_cp = selected_years_GDPgrowthrate
    start_index_cp = df_GDPCP.columns.get_loc(start_year_cp)
    end_index_cp = df_GDPCP.columns.get_loc(end_year_cp)

    # _____Calculate the percentage change for the selected range of years in the first dataframe (df_cp)
    percentage_change_GDPCP = ((df_GDPCP.iloc[0, end_index_cp] - df_GDPCP.iloc[0, start_index_cp]) / df_GDPCP.iloc[
        0, start_index_cp]) * 100

    # ____Finding the corresponding indices for the selected years in the second dataframe (df_kp)
    start_year_kp, end_year_kp = selected_years_GDPgrowthrate
    start_index_kp = df_kp.columns.get_loc(start_year_kp)
    end_index_kp = df_kp.columns.get_loc(end_year_kp)

    # ____Calculating the percentage change for the selected range of years in the second dataframe (df_kp)
    percentage_change_kp = ((df_kp.iloc[0, end_index_kp] - df_kp.iloc[0, start_index_kp]) / df_kp.iloc[
        0, start_index_kp]) * 100

    # ____Displaying the percentage change for GDP at Current prices and GDP at Constant 2017 prices
    st.write(f'Economic growth at Current pricesㅤwas ㅤ{percentage_change_GDPCP:.2f}%')
    st.write(f'Economic growth at Constant 2017 pricesㅤwasㅤ {percentage_change_kp:.2f}%')

    # __Growth rate by kind of activity

    # __Economic growth__

    # __Growth rate by kind of activity
    # _____Define the rows to plot
    rows_to_plot_kp = [2, 8, 22, 38]

    # _____Create a single line graph for all rows
    fig_GDPgrowthrate_by_activity = go.Figure()

    # ____Adding a line for each row to the graph with custom colors
    colors = ['#2E578A', 'green', '#C10000', 'purple']  # Customize the colors based on your preference

    for i, row_index in enumerate(rows_to_plot_kp):
        item_kp = df_kp.iloc[row_index, 0]
        x_values_kp = df_kp.columns[2:].astype(int)
        y_values_kp = df_kp.iloc[row_index, 2:].astype(float)

        # ____Adding the line to the graph with custom color
        fig_GDPgrowthrate_by_activity.add_trace(
            go.Scatter(x=x_values_kp, y=y_values_kp, mode='lines', name=item_kp, line=dict(color=colors[i])))

    # _____Updating the layout
    fig_GDPgrowthrate_by_activity.update_layout(title='Growth by Activity (at constant 2017 prices)',
                                                xaxis_title='Year',
                                                yaxis_title='GDP by activity in Frw billions')

    # ____Showing the line graph
    st.plotly_chart(fig_GDPgrowthrate_by_activity)

  #SLIDER GROWTH RATE BY KIND OF ACTIVITY
    st.caption("Use the slider below to select the specific range of your choice to see its growth rate by activity")


    # _____Function to calculate the percentage change for a specific row and selected years
    def calculate_percentage_change(data, start_year, end_year, row_index):
        start_index = data.columns.get_loc(start_year)
        end_index = data.columns.get_loc(end_year)
        percentage_change = ((data.iloc[row_index, end_index] - data.iloc[row_index, start_index]) / data.iloc[
            row_index, start_index]) * 100
        return percentage_change

        # _____Add a slider to select the range of years


    selected_years_all = st.slider('Select Range of Years', min_value=1999, max_value=2022, value=(1999, 2020))

    # _____Define new row names
    row_names = {2: 'AGRICULTURE, FORESTRY & FISHING', 8: 'INDUSTRY', 22: 'SERVICES',
                 38: 'TAXES LESS SUBSIDIES ON PRODUCTS'}

    # _____Displaying percentage changes for each renamed row below the slider
    for row_index, new_row_name in row_names.items():
        percentage_change = calculate_percentage_change(df_kp, selected_years_all[0], selected_years_all[1], row_index)
        st.write(f'Growth rate for {new_row_name}ㅤwas ㅤ {percentage_change:.2f}%')

    import streamlit as st


    # __NOMINAL VS REAL GDP
    # ____Function to convert nominal value to real value and vice versa
    def convert_values(input_value, is_nominal_to_real=True):
        if is_nominal_to_real:
            return float(input_value) * (10593 / 13716)
        else:
            return float(input_value) / (10593 / 13716)

        # ____Seting up the layout


    st.write('##### 4. Nominal vs Real GDP')
    st.markdown(
        "by looking at the Nominal GDP(13,716 Frw billions) and Real GDP [measured at constant 2017 prices(10,593 Frw billions)]"
        " you can see the impact of inflation on the overall value of goods and services produced within Rwanda.")
    st.caption("The below Nominal/Real GDP converter lets you input and convert different economic values."
               "You can compute and compare the nominal(current Frw prices) and real(measured at constant 2017 Frw prices) GDP")

    # ____Creating two input boxes for nominal and real values

    col1, col2 = st.columns(2)

    with col1:
        nominal_value = st.text_input(label='from Nominal to Real(Rwf)', key='nominal')
        if nominal_value:
            try:
                real_value = convert_values(nominal_value, is_nominal_to_real=True)
                st.write(f"#### {real_value} Rwf")
            except ValueError:
                st.write("Real Value:")

    with col2:
        real_value = st.text_input(label='from Real to Nominal(Rwf)', key='real')
        if real_value:
            try:
                nominal_value = convert_values(real_value, is_nominal_to_real=False)
                st.write(f"#### {nominal_value} Rwf")
            except ValueError:
                st.write("Nominal Value:")


    # __CONSUMER PRICE INDEX___
    st.write("###   ")
    st.write("###   ")
    st.markdown('<h3>🛒 CONSUMER PRICE INDEX</h3>', unsafe_allow_html=True)

    #GENERAL PRICE INDICES

    # Custom CSS for centering the header

    custom_css_header_CPI = """
               <style>
                   .centered-header {
                       text-align: center;
                   }
               </style>
           """

    # Display the custom CSS
    st.markdown(custom_css_header_CPI, unsafe_allow_html=True)

    # Centered header using custom class

    # Custom colors for component
    custom_color_1_CPI = "rgba(46, 87, 138, 0.09)"  # You can change this color code
    custom_color_2_CPI = "rgba(46, 87, 138, 0.2)"  # You can change this color code
    custom_color_3_CPI = "rgba(46, 87, 138, 0.09)"  # You can change this color code

    # Custom CSS for styling the components
    custom_css_CPI = f"""
               <style>
                   .custom-message-g {{
                       background-color: {custom_color_1_CPI};
                       color: auto;
                       padding: 8px;
                       border-radius: 5px;
                       text-align: center;
                   }}

                   .custom-message-h {{
                       background-color: {custom_color_2_CPI};
                       color: auto;
                       padding: 8px;
                       border-radius: 5px;
                       text-align: center;
                   }}

                   .custom-message-j {{
                       background-color: {custom_color_3_CPI};
                       color: auto;
                       padding: 8px;
                       border-radius: 5px;
                       text-align: center;
                   }}
               </style>
           """

    # Display the custom CSS
    st.markdown(custom_css_CPI, unsafe_allow_html=True)

    # Custom content for info and success messages
    info_content1_CPI = """
               <div class="custom-message-g">
                   <div style="font-size: 14px;">Urban CPI</div>
                   <div style="font-size: 36px;">157.8</div>
                   <div style="font-size: 14px;"></div>
               </div>
           """

    success_content2_CPI = """
               <div class="custom-message-h">
                   <div style="font-size: 14px;">Rwanda CPI</div>
                   <div style="font-size: 36px;">180.9</div>
                   <div style="font-size: 14px;"></div>
               </div>
           """

    success_content3_CPI = """
               <div class="custom-message-j">
                   <div style="font-size: 14px;">Rural CPI</div>
                   <div style="font-size: 36px;">196.6</div>
                   <div style="font-size: 14px;"></div>
               </div>
           """

    # Display custom info and success messages

    st.write("###### General Price Indices [index(Feb 2014=100)]")
    col7, col8, col9 = st.columns([15, 20, 15])

    with col7:
        st.markdown(info_content1_CPI, unsafe_allow_html=True)

    with col8:
        st.markdown(success_content2_CPI, unsafe_allow_html=True)

    with col9:
        st.markdown(success_content3_CPI, unsafe_allow_html=True)

    # __Change in CPI
    # _____Extract data for the line graphs
    x = list(df_cpirda.columns[2:])
    y1 = df_cpirda.iloc[1, 2:].values
    y2 = df_cpiurban.iloc[1, 2:].values
    y3 = df_cpirural.iloc[1, 2:].values

    # ____Create traces for each line graph with custom colors and opacity
    trace1 = go.Scatter(x=x, y=y3, mode='lines', name='RURAL GENERAL INDEX (CPI)',
                        line=dict(color='rgba(160, 213, 234, 0.4)'))
    trace2 = go.Scatter(x=x, y=y2, mode='lines', name='URBAN GENERAL INDEX (CPI)',
                        line=dict(color='rgba(249, 170, 170, 0.4)'))
    trace3 = go.Scatter(x=x, y=y1, mode='lines', name='RWANDA GENERAL INDEX (CPI)',
                        line=dict(color='rgba(46, 87, 250, 1)'))

    # ... (your existing code)

    # ____Create layout
    layout = go.Layout(title="Change in General CPI over time (reference: February 2014=100)", xaxis=dict(title='Year(s)'), yaxis=dict(title='GENERAL INDEX (CPI)', range=[80, 200]))

    # ____Create figure and plot
    fig = go.Figure(data=[trace1, trace2, trace3], layout=layout)

    # ____Display the plot using Streamlit
    st.plotly_chart(fig)

    st.caption("On average, prices for consumer goods and services in Rwanda have increased by 80.9% since 2014")

    # __CONSUMER PRICE INDEX___



    # __COMPONENTS OF RWANDA CPI

    st.write('##### 2. components of Rwanda CPI')
    st.markdown("These components collectively represent Rwanda basket of goods and services, "
                "with Food and non-alcoholic beverages contributing the most (39%) to the national basket of goods and services.")

    st.caption("In the box below you can see and select specific CPI components to see their weights, "
                "each bar graph will display the component's relative weights in the Rwanda's basket of goods and services.")

    # ... (your existing code)

    # _____Get the list of available options
    available_items = list(df_cpirda.iloc[[2, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18], 0])

    # _____Default items to be displayed on the chart
    default_items = ['Food and non-alcoholic beverages', 'Alcoholic beverages and tobacco',
                     'Housing, water, electricity, gas and other fuels', 'Transport']

    # _____Check if default items are in the available options, add them if not
    default_items = [item for item in default_items if item in available_items]

    # _____Add a multiselect box with default values
    selected_items = st.multiselect('Select Items to Display', available_items, default=default_items)

    # ... (your existing code)

    # _____Add a color picker for customizing bar color
    # selected_bar_color = st.color_picker('Select Bar Color', default_bar_color)

    # _____Extract data for the bar graph based on the selected items
    filtered_data = df_cpirda[df_cpirda.iloc[:, 0].isin(selected_items)]

    # _____Extract data for the bar graph
    items = filtered_data.iloc[:, 0].values
    values = filtered_data.iloc[:, 1].values

    # _____Create a bar graph with custom bar color and display values in percentages
    formatted_values = [f'{round(val, 1)}%' for val in (values * 1 / 100)]
    fig2 = go.Figure([go.Bar(x=values, y=items, orientation='h', marker_color='#2E578A', text=formatted_values,
                             textposition='auto')])

    # _____Customize the layout
    fig2.update_layout(title_text='Weights of the selected components', xaxis_title='Weights in percentages', yaxis_title='Components')

    st.plotly_chart(fig2)

    #SHOWING DATA SETS_______________________________________________________________________________________________________________________________





if selected == "Data":
    # space_function
    st.write('#        ')
    # DATA
    # __Part last.Data sets___
    st.info("### DATA SETs")
    # Display the CPI data in Streamlit
    st.write('GDP at current prices')
    st.write(df_GDPCP)
    st.write('GDP at constant 2017 prices')
    st.write(df_kp)
    st.write('GDP by Expenditure')
    st.write(df_expenditure)
    st.write('RWANDA CPI data')
    st.write(df_cpirda)
    st.write('URBAN CPI data')
    st.write(df_cpiurban)
    st.write('RURAL CPI data')
    st.write(df_cpirural)


if selected == "More statistics":
    # MORE
    # __ADDITIONAL STATISTICS ON SIDEBAR__
    st.info('### Additional Statistics')
    if st.checkbox("#### Other Consumer Price Indices in Nov-2022(Urban only)"):
        # Custom CSS for centering the header
        custom_css_header_otherconsumerpriceindices = """
            <style>
                .centered-header {
                    text-align: center;
                }
            </style>
        """

        # Display the custom CSS
        st.markdown(custom_css_header_otherconsumerpriceindices, unsafe_allow_html=True)

        # Centered header using custom class
        st.markdown('<h10 class="centered-header">Base: 2014 (Reference: February 2014=100)</h1>',
                    unsafe_allow_html=True)

        # Custom colors for component
        custom_color_1_otherconsumerpriceindices = "rgba(46, 87, 138, 0.2)"  # You can change this color code
        custom_color_2_otherconsumerpriceindices = "rgba(57, 136, 128, 0.2)"  # You can change this color code
        custom_color_3_otherconsumerpriceindices = "rgba(66, 161, 191, 0.2)"  # You can change this color code
        custom_color_4_otherconsumerpriceindices = "rgba(28, 141, 197, 0.2)"  # You can change this color code

        # Custom CSS for styling the components
        custom_css_otherconsumerpriceindices = f"""
            <style>
                .custom-message-1 {{
                    background-color: {custom_color_1_otherconsumerpriceindices};
                    color: auto;
                    padding: 8px;
                    border-radius: 5px;
                    text-align: center;
                }}

                .custom-message-2 {{
                    background-color: {custom_color_2_otherconsumerpriceindices};
                    color: auto;
                    padding: 8px;
                    border-radius: 5px;
                    text-align: center;
                }}

                .custom-message-3 {{
                    background-color: {custom_color_3_otherconsumerpriceindices};
                    color: auto;
                    padding: 8px;
                    border-radius: 5px;
                    text-align: center;
                }}

                .custom-message-4 {{
                    background-color: {custom_color_4_otherconsumerpriceindices};
                    color: auto;
                    padding: 8px;
                    border-radius: 5px;
                    text-align: center;
                }}
            </style>
        """

        # Display the custom CSS
        st.markdown(custom_css_otherconsumerpriceindices, unsafe_allow_html=True)

        # Custom content for info and success messages
        info_content1_otherconsumerpriceindices = """
            <div class="custom-message-1">
                <div style="font-size: 14px;">Local Goods Index</div>
                <div style="font-size: 36px;">154.9</div>
                <div style="font-size: 14px;"></div>
            </div>
        """

        success_content2_otherconsumerpriceindices = """
            <div class="custom-message-2">
                <div style="font-size: 14px;">Imported Goods Index</div>
                <div style="font-size: 36px;">168</div>
                <div style="font-size: 14px;"></div>
            </div>
        """

        success_content3_otherconsumerpriceindices = """
            <div class="custom-message-3">
                <div style="font-size: 14px;">Fresh Products Index</div>
                <div style="font-size: 36px;">217.3</div>
                <div style="font-size: 14px;"></div>
            </div>
        """

        success_content4_otherconsumerpriceindices = """
            <div class="custom-message-4">
                <div style="font-size: 14px;">Energy Index</div>
                <div style="font-size: 36px;">162.9</div>
                <div style="font-size: 14px;"></div>
            </div>
        """

        # Display custom info and success messages
        col1_otherconsumerpriceindices, col2_otherconsumerpriceindices, col3_otherconsumerpriceindices, col4_otherconsumerpriceindices = st.columns(
            4)

        with col1_otherconsumerpriceindices:
            st.markdown(info_content1_otherconsumerpriceindices, unsafe_allow_html=True)

        with col2_otherconsumerpriceindices:
            st.markdown(success_content2_otherconsumerpriceindices, unsafe_allow_html=True)

        with col3_otherconsumerpriceindices:
            st.markdown(success_content3_otherconsumerpriceindices, unsafe_allow_html=True)

        with col4_otherconsumerpriceindices:
            st.markdown(success_content4_otherconsumerpriceindices, unsafe_allow_html=True)

        st.write("###      ")
        st.write("###      ")



    if st.checkbox("#### National income and expenditure (Rwf billions)"):
        # Custom CSS for centering the header
        custom_css_header_Ni = """
            <style>
                .centered-header {
                    text-align: center;
                }
            </style>
        """

        # Display the custom CSS
        st.markdown(custom_css_header_Ni, unsafe_allow_html=True)

        # Centered header using custom class

        # Custom colors for component
        custom_color_1_Ni = "rgba(46, 87, 138, 0.2)"  # You can change this color code
        custom_color_2_Ni = "rgba(46, 87, 138, 0.09)"  # You can change this color code
        custom_color_3_Ni = "rgba(255,0,0, 0.03)"  # You can change this color code

        # Custom CSS for styling the components
        custom_css_Ni = f"""
            <style>
                .custom-message-1 {{
                    background-color: {custom_color_1_Ni};
                    color: auto;
                    padding: 8px;
                    border-radius: 5px;
                    text-align: center;
                }}

                .custom-message-2 {{
                    background-color: {custom_color_2_Ni};
                    color: auto;
                    padding: 8px;
                    border-radius: 5px;
                    text-align: center;
                }}

                .custom-message-3 {{
                    background-color: {custom_color_3_Ni};
                    color: auto;
                    padding: 8px;
                    border-radius: 5px;
                    text-align: center;
                }}
            </style>
        """

        # Display the custom CSS
        st.markdown(custom_css_Ni, unsafe_allow_html=True)

        # Custom content for info and success messages
        info_content1_Ni = """
            <div class="custom-message-1">
                <div style="font-size: 14px;">Gross Ntional Disposable Income</div>
                <div style="font-size: 36px;">14,437</div>
                <div style="font-size: 14px;">(GNI + Current Transfers, net)</div>
            </div>
        """

        success_content2_Ni = """
            <div class="custom-message-2">
                <div style="font-size: 14px;">Gross National Saving</div>
                <div style="font-size: 36px;">1,966</div>
                <div style="font-size: 14px;">(Gross National Disposable Income - Final Consumption Expenditure)</div>
            </div>
        """

        success_content3_Ni = """
            <div class="custom-message-3">
                <div style="font-size: 14px;">Net Lending to the rest of the world</div>
                <div style="font-size: 36px;">-1,393</div>
                <div style="font-size: 14px;">(Gross National Saving - Gross Capital Formation)</div>
            </div>
        """

        # Display custom info and success messages
        cold, colf, colh = st.columns([17, 20, 20])

        with cold:
            st.markdown(info_content1_Ni, unsafe_allow_html=True)

        with colf:
            st.markdown(success_content2_Ni, unsafe_allow_html=True)

        with colh:
            st.markdown(success_content3_Ni, unsafe_allow_html=True)

        st.write("###      ")
        st.write("###      ")

    if st.checkbox("#### Exchange rate"):
        # Custom CSS for centering the header
        custom_css_header_a = """
            <style>
                .centered-header {
                    text-align: center;
                }
            </style>
        """

        # Display the custom CSS
        st.markdown(custom_css_header_a, unsafe_allow_html=True)

        # Custom colors for component
        custom_color_1 = "rgba(46, 87, 138, 0.2)"  # You can change this color code
        custom_color_2 = "rgba(46, 87, 138, 0.2)"  # You can change this color code
        custom_color_3 = "rgba(46, 87, 138, 0.2)"  # You can change this color code
        custom_color_4 = "rgba(46, 87, 138, 0.2)"  # You can change this color code

        # Custom CSS for styling the components
        custom_css = f"""
            <style>
                .custom-message-1 {{
                    background-color: {custom_color_1};
                    color: auto;
                    padding: 8px;
                    border-radius: 5px;
                    text-align: center;
                }}
            </style>
        """

        # Display the custom CSS
        st.markdown(custom_css, unsafe_allow_html=True)

        # Custom content for info and success messages
        info_content1 = """
            <div class="custom-message-1">
                <div style="font-size: 14px;">  Exchange rate</div>
                <div style="font-size: 36px;">1,031</div>
                <div style="font-size: 14px;">Rwf per US dollar</div>
            </div>
        """

        success_content2 = """
            <div class="custom-message-2">
                <div style="font-size: 14px;">Imported Goods Index</div>
                <div style="font-size: 36px;">168</div>
                <div style="font-size: 14px;"></div>
            </div>
        """

        # Display custom info and success messages
        col1, col2, col3 = st.columns(3)

        with col1:
            st.markdown(info_content1, unsafe_allow_html=True)
        st.write("###      ")
        st.write("###      ")



    if st.checkbox("#### 2022 GDP growth by quarters"):

        # GDP growth by quarter data
        quarters = ['First Quarter', 'Second Quarter', 'Third Quarter', 'Fourth Quarter']
        values_quarters = [7.9, 7.5, 10, 7.3]

        # Define custom colors for each bar
        custom_colors_quarters = ['#2E578A', '#2E578A', '#2E578A', '#2E578A']  # You can change these color codes

        # Create a bar graph with custom colors
        fig_GDP_growth_by_quarter = go.Figure(data=[go.Bar(
            x=quarters,
            y=values_quarters,
            text=values_quarters,
            textposition='auto',
            textfont=dict(size=30),
            marker_color=custom_colors_quarters
        )])

        # Update layout
        fig_GDP_growth_by_quarter.update_layout(
            title='2022 GDP growth by quarter',
            xaxis_title='Quarter',
            yaxis_title='% increase',
            yaxis=dict(range=[0, 100])  # Set the y-axis range from 0 to 50
        )

        # Display the bar graph
        st.plotly_chart(fig_GDP_growth_by_quarter)
        st.caption("Measured at constant 2017 prices the year 2022 to grow by 8.2 % when compared to 2021. "
                   "                                           below are 2022 GDP growth by each quarter")


#ENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDENDEND
st.write("#                                        ")
st.write("#                                        ")
st.write("#                                        ")

st.caption("_________________________________________________________________________________________________________")




# Add an image to the sidebar
col1, col2, col3 = st.columns(3)
image1 = Image.open('images/NISR.png')
image3 = Image.open('images/statslab logo a.jpg')
col1.image(image1,
         caption= 'NISR',
         width=75)

col3.image(image3,
         caption= 'STATSLAB',
         width=75)


st.caption("### Source links")
st.caption("Gross Domestic Product 2022 (GDP) and Consumer Price Index 2022 (CPI). Accessed from www.statistics.gov.rw")
st.caption("GDP National Accounts, 2022: https://www.statistics.gov.rw/publication/1914")
st.caption("Consumer Price Index (CPI) - November 2022: https://www.statistics.gov.rw/publication/1873")