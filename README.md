# Creating-payment-receipts-
Creating Payment Receipts with Python and ReportLab
Generating payment receipts is a common task in various applications, whether it's for e-commerce websites or local stores. In this project, we'll explore how to create transaction receipts using Python with the ReportLab library.

Approach
Import Module: We'll start by importing the necessary modules, including ReportLab.

Prepare Data: We need the data in the form of a list of lists, where the 0th index of the outer list represents the headers.

Create Document Template: We'll create a SimpleDocTemplate with the specified paper size, which is A4 in this case.

Apply Styling: Using a sample style sheet from the built-in styles, we'll define the styling for the receipt, such as font, alignment, and colors.

Generate PDF: Finally, we'll feed the data and the style sheet to the PDF object and build it to generate the payment receipt in PDF format.

Code Overview
python
Copy code
# Importing necessary modules
from reportlab.platypus import SimpleDocTemplate, Table, Paragraph, TableStyle
from reportlab.lib import colors
from reportlab.lib.pagesizes import A4
from reportlab.lib.styles import getSampleStyleSheet

# Data for the receipt
DATA = [
    ["Date", "Name", "Subscription", "Price (Rs.)"],
    ["07/04/2024", "Data and Analytics",
        "Lifetime", "10,999.00/-"],
    ["07/04/2024", "Power BI", "6 months", "3,999.00/-"],
    ["Sub Total", "", "", "14998.00/-"],
    ["Discount", "", "", "-998.00/-"],
    ["Total", "", "", "14000.00/-"],
]


# Creating a SimpleDocTemplate with A4 page size
pdf = SimpleDocTemplate("receipt.pdf", pagesize=A4)

# Getting sample styles from ReportLab
styles = getSampleStyleSheet()

# Fetching the style for top-level heading (Heading1)
title_style = styles["Heading1"]

# Aligning the heading to center
title_style.alignment = 1

# Creating a paragraph with the heading text and applying the styles
title = Paragraph("pyc coder", title_style)

# Creating TableStyle object and defining styles row-wise
style = TableStyle(
    [
        ("BOX", (0, 0), (-1, -1), 1, colors.black),
        ("GRID", (0, 0), (4, 4), 1, colors.black),
        ("BACKGROUND", (0, 0), (3, 0), colors.gray),
        ("TEXTCOLOR", (0, 0), (-1, 0), colors.whitesmoke),
        ("ALIGN", (0, 0), (-1, -1), "CENTER"),
        ("BACKGROUND", (0, 1), (-1, -1), colors.beige),
    ]
)

# Creating a table object and applying the defined style
table = Table(DATA, style=style)

# Building the final PDF by adding the title and table
pdf.build([title, table])
How to Use
Clone or download the repository to your local machine.

Make sure you have Python and ReportLab installed.

Modify the DATA variable to include your transaction details.

Run the Python script, and it will generate a PDF file containing the payment receipt.

Dependencies
Python 3.x
ReportLab
License
This project is licensed under the MIT License. See the LICENSE file for details.
