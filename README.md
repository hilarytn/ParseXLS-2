
## Application Features and Line Visualization Page Guide

### Introduction
The application is designed to handle Excel file uploads, process the data, and provide visualizations for better understanding. This guide provides an overview of the application's features and functionalities, including a detailed description of the Line Visualization page.

### Application Features

#### Excel File Handling
- Users can upload Excel files containing production data.
- The application processes the uploaded files and updates the master file and line-specific files accordingly.
- Data cleanup functionality is available to remove uploaded files after processing.

#### User Authentication
- Users can register for an account or log in using their credentials.
- Authentication ensures that only authorized users can access the application's functionalities.

#### Data Visualization
- The application provides visualizations to help users analyze production line data effectively.

### Line Visualization Page

#### Line Information
- Upon accessing the Line Visualization page, users are greeted with information about the specific production line, identified by its number.

#### Download and Navigation
- Users can download data related to the current production line by clicking the "Download Line {{ line_number }}" button.
- The "Go Back" button redirects users to the Home page.
- The "Go To Visualization" button navigates users to the visualization section on the page.

#### Data Table
- The data table displays detailed information about each entry related to the production line, including:
  - Line number
  - Date
  - Description
  - Start time
  - End time
  - Time gap
  - Downtime

#### Visualization
- **Pie Chart**: Presents the distribution of product percentages based on the data associated with the production line.
- **Bar Chart**: Illustrates the aggregated time gap and downtime for each product.
- **Bar Chart (Tgaps and Count)**: Visualizes the time gaps and counts for each product.

#### Instructions
1. **Download Line Data**:
   - Click the "Download Line {{ line_number }}" button to download data related to the current production line.

2. **Navigation**:
   - Use the "Go Back" button to return to the Home page.
   - Click the "Go To Visualization" button to quickly navigate to the visualization section.

3. **Data Table**:
   - Review the detailed information provided in the data table.

4. **Visualization**:
   - Interpret the pie chart, bar chart, and tgaps/count chart to gain insights into the production line's performance.

   <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Excel</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
</head>
<body>
    <div class="container mt-3">
        <h2>Smart Wash Data Dashboard Input</h2>
        <br>
        <!-- Nav tabs -->
        <ul class="nav nav-tabs" role="tablist">
            <li class="nav-item">
                <a class="nav-link active" data-bs-toggle="tab" href="#facility1">Facility 1</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" data-bs-toggle="tab" href="#facility2">Facility 2</a>
            </li>
        </ul>

        <!-- Tab panes -->
        <div class="tab-content">
            <!-- Facility 1 tab pane -->
            <div id="facility1" class="container tab-pane active"><br>
                <h3>Facility 1</h3>
                <!-- File upload form for Facility 1 -->
                <form action="/upload_facility1" method="post" enctype="multipart/form-data">
                    <label for="file-upload-facility1" class="form-label">Choose Files for Facility 1</label>
                    <input id="file-upload-facility1" class="form-control" type="file" name="files[]" multiple accept=".xls,.xlsx" required>
                    <button type="submit" class="btn btn-primary mt-2">Upload</button>
                </form>
                <!-- Facility 1 upload history table goes here -->
                <h4>Facility 1 Upload History</h4>
                <table class="table">
                    <thead>
                        <tr>
                            <th>File Name</th>
                            <th>Upload Date</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- Populate this table dynamically with data from Flask -->
                    </tbody>
                </table>
            </div>

            <!-- Facility 2 tab pane -->
            <div id="facility2" class="container tab-pane fade"><br>
                <h3>Facility 2</h3>
                <!-- File upload form for Facility 2 -->
                <form action="/upload_facility2" method="post" enctype="multipart/form-data">
                    <label for="file-upload-facility2" class="form-label">Choose Files for Facility 2</label>
                    <input id="file-upload-facility2" class="form-control" type="file" name="files[]" multiple accept=".xls,.xlsx" required>
                    <button type="submit" class="btn btn-primary mt-2">Upload</button>
                </form>
                <!-- Facility 2 upload history table goes here -->
                <h4>Facility 2 Upload History</h4>
                <table class="table">
                    <thead>
                        <tr>
                            <th>File Name</th>
                            <th>Upload Date</th>
                        </tr>
                    </thead>
                    <tbody>
                        <!-- Populate this table dynamically with data from Flask -->
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Excel</title>
    <link rel="icon" href="{{ url_for('static', filename='img/favicon.jpg') }}" type="image/x-icon">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
    <style>
        .container {
            box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
            padding: 20px;
            background-color: #f9f9f9;
            border-radius: 8px;
        }
        .file-upload-btn {
            background-color: #333;
            border: none;
            color: #fff;
            padding: 10px 20px;
            border-radius: 4px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .file-upload-btn:hover {
            background-color: #555;
        }
    </style>
</head>
<body>
    <div class="container mt-3">
        <h2>Smart Wash Data Dashboard Input</h2>
        <br>
        <!-- Nav tabs -->
        <ul class="nav nav-tabs" role="tablist">
            <li class="nav-item">
                <a class="nav-link active" data-bs-toggle="tab" href="#facility1">Facility 1</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" data-bs-toggle="tab" href="#facility2">Facility 2</a>
            </li>
        </ul>

        <!-- Tab panes -->
        <div class="tab-content">
            <!-- Facility 1 tab pane -->
            <div id="facility1" class="container tab-pane active"><br>
                <h3>Facility 1</h3>
                <!-- Tab panes for Source 1 and Source 2 -->
                <ul class="nav nav-tabs" role="tablist">
                    <li class="nav-item">
                        <a class="nav-link active" data-bs-toggle="tab" href="#facility1_source1">Source 1</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" data-bs-toggle="tab" href="#facility1_source2">Source 2</a>
                    </li>
                </ul>
                <!-- Tab content for Source 1 and Source 2 -->
                <div class="tab-content">
                    <div id="facility1_source1" class="container tab-pane active"><br>
                        <!-- File upload form for Facility 1 - Source 1 -->
                        <form action="/upload_facility1_source1" method="post" enctype="multipart/form-data">
                            <label for="file-upload-facility1-source1" class="form-label">Choose Files for Source 1</label>
                            <input id="file-upload-facility1-source1" class="form-control" type="file" name="files[]" multiple accept=".xls,.xlsx" required>
                            <button type="submit" class="btn btn-primary mt-2 file-upload-btn">Upload</button>
                        </form>
                        <!-- Upload history table for Facility 1 - Source 1 -->
                        <h4>Facility 1 - Source 1 Upload History</h4>
                        <table class="table">
                            <thead>
                                <tr>
                                    <th>File Name</th>
                                    <th>Upload Date</th>
                                </tr>
                            </thead>
                            <tbody>
                                <!-- Populate this table dynamically with data from Flask -->
                            </tbody>
                        </table>
                    </div>
                    <div id="facility1_source2" class="container tab-pane fade"><br>
                        <!-- File upload form for Facility 1 - Source 2 -->
                        <form action="/upload_facility1_source2" method="post" enctype="multipart/form-data">
                            <label for="file-upload-facility1-source2" class="form-label">Choose Files for Source 2</label>
                            <input id="file-upload-facility1-source2" class="form-control" type="file" name="files[]" multiple accept=".xls,.xlsx" required>
                            <button type="submit" class="btn btn-primary mt-2 file-upload-btn">Upload</button>
                        </form>
                        <!-- Upload history table for Facility 1 - Source 2 -->
                        <h4>Facility 1 - Source 2 Upload History</h4>
                        <table class="table">
                            <thead>
                                <tr>
                                    <th>File Name</th>
                                    <th>Upload Date</th>
                                </tr>
                            </thead>
                            <tbody>
                                <!-- Populate this table dynamically with data from Flask -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- Facility 2 tab pane -->
            <div id="facility2" class="container tab-pane fade"><br>
                <h3>Facility 2</h3>
                <!-- Tab panes for Source 1 and Source 2 -->
                <ul class="nav nav-tabs" role="tablist">
                    <li class="nav-item">
                        <a class="nav-link active" data-bs-toggle="tab" href="#facility2_source1">Source 1</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" data-bs-toggle="tab" href="#facility2_source2">Source 2</a>
                    </li>
                </ul>
                <!-- Tab content for Source 1 and Source 2 -->
                <div class="tab-content">
                    <div id="facility2_source1" class="container tab-pane active"><br>
                        <!-- File upload form for Facility 2 - Source 1 -->
                        <form action="/upload_facility2_source1" method="post" enctype="multipart/form-data">
                            <label for="file-upload-facility2-source1" class="form-label">Choose Files for Source 1</label>
                            <input id="file-upload-facility2-source1" class="form-control" type="file" name="files[]" multiple accept=".xls,.xlsx" required>
                            <button type="submit" class="btn btn-primary mt-2 file-upload-btn">Upload</button>
                        </form>
                        <!-- Upload history table for Facility 2 - Source 1 -->
                        <h4>Facility 2 - Source 1 Upload History</h4>
                        <table class="table">
                            <thead>
                                <tr>
                                    <th>File Name</th>
                                    <th>Upload Date</th>
                                </tr>
                            </thead>
                            <tbody>
                                <!-- Populate this table dynamically with data from Flask -->
                            </tbody>
                        </table>
                    </div>
                    <div id="facility2_source2" class="container tab-pane fade"><br>
                        <!-- File upload form for Facility 2 - Source 2 -->
                        <form action="/upload_facility2_source2" method="post" enctype="multipart/form-data">
                            <label for="file-upload-facility2-source2" class="form-label">Choose Files for Source 2</label>
                            <input id="file-upload-facility2-source2" class="form-control" type="file" name="files[]" multiple accept=".xls,.xlsx" required>
                            <button type="submit" class="btn btn-primary mt-2 file-upload-btn">Upload</button>
                        </form>
                        <!-- Upload history table for Facility 2 - Source 2 -->
                        <h4>Facility 2 - Source 2 Upload History</h4>
                        <table class="table">
                            <thead>
                                <tr>
                                    <th>File Name</th>
                                    <th>Upload Date</th>
                                </tr>
                            </thead>
                            <tbody>
                                <!-- Populate this table dynamically with data from Flask -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</body>
</html>


