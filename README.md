# tour_booking

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Travel Booking</title>
    <link rel="stylesheet" href="booking.css">
</head>
<body>

    <header>
        <h1>Travel Hub</h1>
        <nav>
            <ul>
                <li><a href="#">Home</a></li>
                <li><a href="#">About</a></li>
                <li><a href="#">Contact</a></li>
            </ul>
        </nav>
    </header>

    
        <!-- First Card for Input -->
        <div class="card">
            <h2>Travel Booking</h2>

            <label for="name">Name:</label>
            <input type="text" id="name" placeholder="Enter your name">

            <label for="age">Age:</label>
            <input type="number" id="age" placeholder="Enter your age">

            <label for="from">From Location:</label>
            <input type="text" id="from" placeholder="Enter starting location">

            <label for="to">To Location:</label>
            <input type="text" id="to" placeholder="Enter destination">

            <label for="km">KM:</label>
            <input type="number" id="km" placeholder="Enter distance (KM)">

            <label for="price">Price:</label>
            <input type="number" id="price" placeholder="Enter price">

            <div class="button-group">
                <button class="get" onclick="getBooking()">Get Booking</button>
                <button class="book" onclick="addBooking()">Book</button>
                <button class="update" onclick="updateBooking()">Update</button>
                <button class="delete" onclick="deleteBooking()">Delete</button>
            </div>
        </div>

        <!-- Second Card (Card2) with Table -->
        <div class="card2">
            <h2>Booking Details</h2>
            <table id="bookingTable">
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Age</th>
                        <th>From</th>
                        <th>To</th>
                        <th>KM</th>
                        <th>Price</th>
                    </tr>
                    
                </thead>
                <tbody>
                    <!-- New rows will be added here dynamically -->
                </tbody>
            </table>
        </div>
    

    <script src="booking.js"></script>

</body>
</html>



CSS-----



/* General Styles */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, sans-serif;
}

body {
    background-color: #f5f5f5;
    text-align: center;
}

/* Header Styles */
header {
    background-color: #930c97;
    color: white;
    padding: 15px 0;
    text-align: center;
}

nav ul {
    list-style: none;
    padding: 0;
}

nav ul li {
    display: inline;
    margin: 0 15px;
}

nav ul li a {
    color: white;
    text-decoration: none;
    font-weight: bold;
}

/* Main Container */


/* Card Styling */
.card {
    background-color: white;
    padding: 10px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    width: 45%;
    max-width: 500px;
    margin-right: 10%;
}
.card2{
    margin-left: 40%;
    padding: 10px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    width: 45%;
    max-width: 500px;
   
    margin-bottom: 10px;
   

}

h2 {
    margin-bottom: 15px;
    color: #333;
}

/* Input Styles */
label {
    display: block;
    margin-top: 10px;
    text-align: left;
    font-weight: bold;
    color: #555;
}

input {
    width: 100%;
    padding: 8px;
    margin-top: 5px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

/* Button Styles */
.button-group {
    margin-top: 15px;
}

button {
    background-color: #007bff;
    color: white;
    padding: 10px;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    margin: 5px;
    width: 100px;
    font-weight: bold;
}

button:hover {
    background-color: #0056b3;
}

.update {
    background-color: #ffc107;
}

.update:hover {
    background-color: #e0a800;
}

.delete {
    background-color: #dc3545;
}

.delete:hover {
    background-color: #c82333;
}

/* Table Styles */
table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 10px;
}

th, td {
    padding: 10px;
    border: 1px solid #ccc;
    text-align: center;
}

th {
    background-color: #c00ab1;
    color: white;
}

tbody tr:hover {
    background-color: #f1f1f1;
    cursor: pointer;
}

/* Responsive Design */
@media (max-width: 600px) {
    .card {
        width: 95%;
    }
    .card2{
        width: 95%;
    }

    button {
        width: 80px;
    }
}


js-------------
// Function to add a new booking to the table
function addBooking() {
    let name = document.getElementById("name").value;
    let age = document.getElementById("age").value;
    let from = document.getElementById("from").value;
    let to = document.getElementById("to").value;
    let km = document.getElementById("km").value;
    let price = document.getElementById("price").value;

    // Validation: Ensure all fields are filled
    if (name === "" || age === "" || from === "" || to === "" || km === "" || price === "") {
        alert("Please fill in all fields before booking.");
        return;
    }

    // Prepare data for API
    let bookingData = {
        name: name,
        age: parseInt(age), // Convert to integer
        from: from,
        to: to,
        km: parseFloat(km), // Convert to float
        price: parseFloat(price) // Convert to float
    };

    // API call using fetch()
    fetch("http://localhost:8080/Student/addStudent", {
        method: "POST",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify(bookingData)
    })
    .then(response => {
        if (!response.ok) {
            throw new Error("Failed to add booking");
        }
        return response.json();
    })
    .then(data => {
        console.log("Booking added:", data);
        alert("Booking successfully added!");

        // Insert data into table after successful API response
        let table = document.getElementById("bookingTable").getElementsByTagName('tbody')[0];
        let newRow = table.insertRow();
        newRow.innerHTML = `<td>${bookingData.name}</td><td>${bookingData.age}</td><td>${bookingData.from}</td><td>${bookingData.to}</td><td>${bookingData.km}</td><td>${bookingData.price}</td>`;
        newRow.onclick = function() { selectRow(this); };

        // Clear input fields after booking
        clearInputs();
    })
    .catch(error => {
        console.error("Error:", error);
        alert("Error adding booking. Please try again.");
    });
}

// Function to clear input fields
function clearInputs() {
    document.getElementById("name").value = "";
    document.getElementById("age").value = "";
    document.getElementById("from").value = "";
    document.getElementById("to").value = "";
    document.getElementById("km").value = "";
    document.getElementById("price").value = "";
}
function getBooking() {
    let name = document.getElementById("name").value; // Get name input value

    if (name.trim() === "") {
        alert("Please enter a name to search.");
        return;
    }

    fetch(`http://localhost:8080/Student/getStudent?name=${encodeURIComponent(name)}`)
    .then(response => {
        if (!response.ok) {
            throw new Error("No data found for this name.");
        }
        return response.json();
    })
    .then(data => {
        displayBooking(data);
    })
    .catch(error => {
        console.error("Error:", error);
        alert("Error fetching booking details.");
    });
}

// Function to display the fetched data in the table
function displayBooking(data) {
    let tableBody = document.getElementById("bookingTable").getElementsByTagName('tbody')[0];
    tableBody.innerHTML = ""; // Clear existing table data

    let newRow = tableBody.insertRow();
    newRow.innerHTML = `
        <td>${data.name}</td>
        <td>${data.age}</td>
        <td>${data.from}</td>
        <td>${data.to}</td>
        <td>${data.km}</td>
        <td>${data.price}</td>
    `;

    newRow.onclick = function() { selectRow(this); }; // Enable row selection for updates/deletion
}



// Function to update the selected row
function updateBooking() {
    if (!selectedRow) {
        alert("Please select a row to update.");
        return;
    }

    // Get updated values from input fields
    let updatedBooking = {
        name: document.getElementById("name").value,
        age: parseInt(document.getElementById("age").value),
        from: document.getElementById("from").value,
        to: document.getElementById("to").value,
        km: parseFloat(document.getElementById("km").value),
        price: parseFloat(document.getElementById("price").value)
    };

    // API call using fetch()
    fetch("http://localhost:8080/Student/updateStudent", {
        method: "PUT",  // Assuming it's a PUT request for updates
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify(updatedBooking)
    })
    .then(response => {
        if (!response.ok) {
            throw new Error("Failed to update booking");
        }
        return response.json();
    })
    .then(data => {
        console.log("Booking updated:", data);
        alert("Booking successfully updated!");

        // Update the selected row in the table
        let cells = selectedRow.getElementsByTagName("td");
        cells[0].innerText = updatedBooking.name;
        cells[1].innerText = updatedBooking.age;
        cells[2].innerText = updatedBooking.from;
        cells[3].innerText = updatedBooking.to;
        cells[4].innerText = updatedBooking.km;
        cells[5].innerText = updatedBooking.price;

        // Clear selected row
        selectedRow = null;
        clearInputs();
    })
    .catch(error => {
        console.error("Error:", error);
        alert("Error updating booking. Please try again.");
    });
}

// Function to clear input fields
function clearInputs() {
    document.getElementById("name").value = "";
    document.getElementById("age").value = "";
    document.getElementById("from").value = "";
    document.getElementById("to").value = "";
    document.getElementById("km").value = "";
    document.getElementById("price").value = "";
}


function deleteBooking() {
    if (!selectedRow) {
        alert("Please select a row to delete.");
        return;
    }

    // Get the name from the selected row
    let name = selectedRow.getElementsByTagName("td")[0].innerText;

    // API call using fetch()
    fetch(`http://localhost:8080/Student/deleteStudent?name=${encodeURIComponent(name)}`, {
        method: "DELETE"
    })
    .then(response => {
        if (!response.ok) {
            throw new Error("Failed to delete booking");
        }
        return response.text(); // API may return a success message
    })
    .then(data => {
        console.log("Booking deleted:", data);
        alert("Booking successfully deleted!");

        // Remove the row from the table
        selectedRow.remove();
        selectedRow = null;

        // Clear input fields
        clearInputs();
    })
    .catch(error => {
        console.error("Error:", error);
        alert("Error deleting booking. Please try again.");
    });
}

// Function to clear input fields
function clearInputs() {
    document.getElementById("name").value = "";
    document.getElementById("age").value = "";
    document.getElementById("from").value = "";
    document.getElementById("to").value = "";
    document.getElementById("km").value = "";
    document.getElementById("price").value = "";
}


JAVA-----------------------------------------------------------------------------

controler : 

package com.controler;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;
import com.dto.ServiceResponseDto;
import com.dto.con_printVO;
import com.service.con_service;
@CrossOrigin(origins = {"*"})
@RestController
@RequestMapping(path = "/Student")
public class con_controler {
	@Autowired
	private con_service dom_serv;
	@GetMapping("/getStudent")
	public ResponseEntity<List<con_printVO>> getStudent(@RequestParam(value = "name") String name) {
		List<con_printVO> response = new ArrayList<con_printVO>();
		response = dom_serv.getStudent(name);
		return new ResponseEntity<List<con_printVO>>(response, HttpStatus.OK);
	}
	@PostMapping("/addStudent")
	public ResponseEntity<ServiceResponseDto> addStudent(@RequestBody  con_printVO studentdto) {
		ResponseEntity<ServiceResponseDto> servResponse = null;
		ServiceResponseDto response = null;
		try {
			response = new ServiceResponseDto("0000", Arrays.asList(dom_serv.addStudent(studentdto)));
			servResponse = new ResponseEntity<ServiceResponseDto>(response, HttpStatus.OK);
		} catch (RuntimeException e) {
			response = new ServiceResponseDto("1111", Arrays.asList(e.getMessage()));
			servResponse = new ResponseEntity<ServiceResponseDto>(response, HttpStatus.INTERNAL_SERVER_ERROR);
		}
		return servResponse;
	}
	@PutMapping("/updateStudent")
	public ResponseEntity<ServiceResponseDto> updateStudent(@RequestBody  con_printVO studentdto) {
		ResponseEntity<ServiceResponseDto> servResponse = null;
		ServiceResponseDto response = null;
		try {
			response = new ServiceResponseDto("0000", Arrays.asList(dom_serv.updateStudent(studentdto)));
			servResponse = new ResponseEntity<ServiceResponseDto>(response, HttpStatus.OK);
		} catch (RuntimeException e) {
			response = new ServiceResponseDto("1111", Arrays.asList(e.getMessage()));
			servResponse = new ResponseEntity<ServiceResponseDto>(response, HttpStatus.INTERNAL_SERVER_ERROR);
		}
		return servResponse;
	}
	@DeleteMapping("/deleteStudent")
	public ResponseEntity<ServiceResponseDto> deleteStudent(@RequestParam(value = "name") String name) {
		ResponseEntity<ServiceResponseDto> servResponse = null;
		ServiceResponseDto response = null;
		try {
			response = new ServiceResponseDto("0000", Arrays.asList(dom_serv.deleteStudent(name)));
			servResponse = new ResponseEntity<ServiceResponseDto>(response, HttpStatus.OK);
		} catch (RuntimeException e) {
			response = new ServiceResponseDto("1111", Arrays.asList(e.getMessage()));
			servResponse = new ResponseEntity<ServiceResponseDto>(response, HttpStatus.INTERNAL_SERVER_ERROR);
		}
		return servResponse;
	}
	
}

service :

package com.service;

import java.util.List;

import org.springframework.stereotype.Service;

import com.dto.con_printVO;

@Service
public interface con_service  {
	public List<con_printVO> getStudent(String name);
	
		public String addStudent(con_printVO studentdto) ;
		public String updateStudent(con_printVO studentdto);
		public String deleteStudent(String name);

}
seriveImpl---------------


package com.seriveImpl;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import com.DAO.con_DAO;
import com.dto.con_printVO;
import com.service.con_service;
@Component
public class con_serviceImpl implements con_service   {
	@Autowired
	private con_DAO student_dao;


	@Override
	public List<con_printVO> getStudent(String name) {
		
		return student_dao.getStudent(name);
	}
		public String addStudent (con_printVO studentdto) {
		
		return student_dao.addStudent(studentdto);
	}
		public String updateStudent(con_printVO studentdto) {
			return student_dao.updateStudent(studentdto);
		}
		public String deleteStudent(String name) {
			return student_dao.deleteStudent(name);
		}

}

DAO :
package com.DAO;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.util.ArrayList;
import java.util.List;

import org.springframework.stereotype.Repository;

import com.DBconncetion.con_DBconnection;
import com.dto.con_printVO;

@Repository
public class con_DAO {
	List<String> id = new ArrayList<>();
	public List<con_printVO> getStudent(String name){
		Connection connection = null;
		PreparedStatement ps = null;
		ResultSet rs = null;
		String storeProc = "";
		List<con_printVO> al = null;
		al = new ArrayList<con_printVO>();
		try {
			if (connection == null) {
				connection = con_DBconnection.getConnection();
			}
			storeProc = "{call get_produ_in_booking_data(?)}";
			ps = connection.prepareStatement(storeProc);
			ps.setString(1, name);
			rs = ps.executeQuery();
			System.out.println(storeProc);
			while (rs.next()) {
				con_printVO dto = new con_printVO();
				dto.setName(rs.getString(1));
				dto.setAge(rs.getInt(2));
				dto.setFrom(rs.getString(3));
				dto.setTo(rs.getString(4));
				dto.setPrice(rs.getDouble(5));
				dto.setKm(rs.getInt(6));
				al.add(dto);
			}
			System.out.println(id);
			}
			catch (Exception e) {
				System.out.println("Error in  getStudent : " + e.getMessage());
				throw new RuntimeException(e.getMessage());
			}finally {
				if (rs != null) {
					try {
						rs.close();
					} catch (Exception e) {
						;
					}
				}
				if (ps != null) {
					try {
						ps.close();
					} catch (Exception e) {
						;
					}
				}
				if (connection != null) {
					try {
						connection.close();
					} catch (Exception e) {

					}
				}
			}
			return al;
		}
	public String addStudent(con_printVO studentdto) {
		Connection connection = null;
		PreparedStatement ps = null;
		ResultSet rs = null;
		String sql = null, status = null;

		try {
			if (connection == null) {
				connection = con_DBconnection.getConnection();
			}
			sql = "{call insert_produ_in_booking(?,?,?,?,?,?)}";
			ps = connection.prepareStatement(sql);
			ps.setString(1,studentdto.getName());
			ps.setInt(2, studentdto.getAge());
			ps.setString(3, studentdto.getFrom());
			ps.setString(4, studentdto.getTo());
			ps.setDouble(5, studentdto.getPrice());
			ps.setInt(6, studentdto.getKm());
			

			/*
			 * ps.setString(1, studentdto.getS_id()); ps.setString(2,
			 * studentdto.getS_name()); ps.setString(3, studentdto.getS_add());
			 */

			System.out.println(ps.toString());

			rs = ps.executeQuery();

			ps.clearParameters();

			while (rs.next()) {
				status = rs.getString(1);
			}

		} catch (Exception e) {

			System.out.println("addStudent" + e.getMessage());
			throw new RuntimeException(e.getMessage());
		} finally {
			if (rs != null) {
				try {
					rs.close();
				} catch (Exception e) {
					;
				}
				rs = null;
			}
			if (ps != null) {
				try {
					ps.close();
				} catch (Exception e) {
					;
				}
				ps = null;
			}
			if (connection != null) {
				try {
					connection.close();
				} catch (Exception e) {
					;
				}
				connection = null;
			}
		}
		return status;

	}
	public String updateStudent(con_printVO studentdto) {
//		
	Connection connection = null;
	PreparedStatement ps = null;
	ResultSet rs = null;
	String storeProc = null, status = null;
	try {
		if (connection == null) {
			connection = con_DBconnection.getConnection();
		}
		storeProc = "{call update_produ(?,?,?,?,?,?)}";
		ps = connection.prepareStatement(storeProc);
		ps.setString(1, studentdto.getName());
		ps.setInt(2, studentdto.getAge());
		ps.setString(3, studentdto.getFrom());
		ps.setString(4, studentdto.getTo());
		ps.setDouble(5, studentdto.getPrice());
		ps.setInt(6, studentdto.getKm());
		
		
		/*
		 * ps.setString(1, studentdto.getS_id()); ps.setString(2,
		 * studentdto.getS_add());
		 */
		
		rs = ps.executeQuery();

		ps.clearParameters();

		while (rs.next()) {
			status = rs.getString(1);
		}

	} catch (Exception e) {

		System.out.println("updateInvoice" + e.getMessage());
		throw new RuntimeException(e.getMessage());
	} finally {
		if (rs != null) {
			try {
				rs.close();
			} catch (Exception e) {
				;
			}
			rs = null;
		}
		if (ps != null) {
			try {
				ps.close();
			} catch (Exception e) {
				;
			}
			ps = null;
		}
		if (connection != null) {
			try {
				connection.close();
			} catch (Exception e) {
				;
			}
			connection = null;
		}
	}
	return status;

}
	public String deleteStudent(String name) {
		Connection connection = null;
		PreparedStatement ps = null;
		ResultSet rs = null;
		String storeProc = null, status = null;

		try {
			if (connection == null) {
				connection = con_DBconnection.getConnection();
			}
			storeProc = "{call delete_produ(?)}";
			ps = connection.prepareStatement(storeProc);
			ps.setString(1, name);
			System.out.println(ps.toString());

			rs = ps.executeQuery();

			ps.clearParameters();
			 if (rs.next()) {
	                status = rs.getString(1);
	            } else {
	                status = "FAILURE";
	            }

		} catch (Exception e) {

			System.out.println("delectStudent" + e.getMessage());
			throw new RuntimeException(e.getMessage());
		} finally {
			if (rs != null) {
				try {
					rs.close();
				} catch (Exception e) {
					;
				}
				rs = null;
			}
			if (ps != null) {
				try {
					ps.close();
				} catch (Exception e) {
					;
				}
				ps = null;
			}
			if (connection != null) {
				try {
					connection.close();
				} catch (Exception e) {
					;
				}
				connection = null;
			}
		}
		return status;

	}


}

DB-CONNCETION:

package com.DBconncetion;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class con_DBconnection {
	public static Connection getConnection() 
    {
        String url = "jdbc:mysql://localhost:3306/tour_booking";
        String user = "root";
        String password ="root";

        Connection connection = null;

        try {
            
            Class.forName("com.mysql.cj.jdbc.Driver");

           connection = DriverManager.getConnection(url, user, password);

           
                System.out.println("Connected to the database");
            
        } catch (SQLException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } 
		return connection;
    }

}

ServiceResponseDto :
package com.dto;

import java.util.List;
import com.fasterxml.jackson.annotation.JsonProperty;
public class ServiceResponseDto {
	public ServiceResponseDto(String message, List<String> description) {
		super();
		this.message = message;
		this.description = description;
	}



	@JsonProperty("messagecode")
	private String message;
	
	@JsonProperty("message")
	private List<String> description;

}







