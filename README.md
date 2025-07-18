# pixar_films

# 🎬 Pixar Films Data Analysis Project

This project presents a complete exploratory and analytical study of Pixar films using SQL.  
The dataset includes detailed information about movies, people involved, genres, box office performance, public reception, and awards.

---

## 📁 Dataset Overview

The dataset contains the following tables:

- `pixar_films`: Basic details about each film including title, release date, run time, rating, and plot summary.
- `pixar_people`: Information about directors, producers, and other key people involved in the films.
- `genres`: Subgenres and category types of each film.
- `box_office`: Budget and box office earnings (US/Canada, other countries, worldwide).
- `public_response`: Critic and user scores from Rotten Tomatoes, Metacritic, and IMDb.
- `academy`: Academy Award nominations and wins for each film.

---

## 🧠 Project Goals

- Clean and explore the Pixar dataset
- Answer business and analytical questions using SQL
- Calculate ROI, average ratings, award win percentages
- Group films by budget categories and franchises
- Identify top-performing subgenres, directors, and film series

---

## 📊 Key Analyses & Insights

Here are some of the SQL tasks covered in this project:

- ✅ **Convert budgets and revenue to millions**, and format scores as percentages
- ✅ **Calculate ROI** (Return on Investment) for each film
- ✅ **Find the most profitable subgenres** (appeared in at least 3 films)
- ✅ **Director performance** based on average IMDb, Rotten Tomatoes, and revenue
- ✅ **Compare performance of franchises** like *Toy Story*, *Cars*, and *Finding Nemo/Dory*
- ✅ **Win percentage** of Academy Awards per film
- ✅ **Group films into budget categories** (Low, Medium, High)
- ✅ **Find the best selling month per year** using window functions

---

## 🧼 Data Cleaning

- Removed rows with NULL values in critical columns
- Standardized date formats using `STR_TO_DATE()`
- Converted budgets and worldwide grosses to millions
- Added new columns with formatted percentage strings where needed

---

## 🛠️ Tools Used

- **MySQL** (Workbench)
- **Excel** (for initial data formatting and CSV export)
- **GitHub** (for version control and project hosting)

---

## 📁 File Structure

