create datagram socket and it's method in java

import java.net.DatagramSocket;
import java.net.DatagramPacket;
import java.net.InetAddress;

public class DatagramSocketExample {
    public static void main(String[] args) {
        try {
            // Create a DatagramSocket
            DatagramSocket socket = new DatagramSocket();

            // Sending data
            String message = "Hello, Datagram Socket!";
            byte[] sendData = message.getBytes();
            InetAddress serverAddress = InetAddress.getByName("localhost"); // Replace with the server's address
            int serverPort = 12345; // Replace with the server's port

            DatagramPacket sendPacket = new DatagramPacket(sendData, sendData.length, serverAddress, serverPort);
            socket.send(sendPacket);

            // Receiving data
            byte[] receiveData = new byte[1024];
            DatagramPacket receivePacket = new DatagramPacket(receiveData, receiveData.length);
            socket.receive(receivePacket);

            String receivedMessage = new String(receivePacket.getData(), 0, receivePacket.getLength());
            System.out.println("Received: " + receivedMessage);

            // Close the DatagramSocket
            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

---------------------------------------------------------------------------------
how to a get file size from the server

import java.io.IOException;
import java.net.HttpURLConnection;
import java.net.URL;

public class GetFileSizeFromServer {
    public static void main(String[] args) {
        try {
            // Replace this URL with the URL of the file on the server
            URL url = new URL("https://example.com/path/to/your/file.txt");

            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("HEAD");

            int responseCode = connection.getResponseCode();

            if (responseCode == HttpURLConnection.HTTP_OK) {
                // Get the file size from the "Content-Length" header
                int fileSize = connection.getContentLength();
                System.out.println("File Size: " + fileSize + " bytes");
            } else {
                System.out.println("HTTP request failed with response code: " + responseCode);
            }

            connection.disconnect();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

-----------------------------------------------------------------------------------------------

how to change a host name is specific id address

import java.net.InetAddress;

public class HostnameChange {
    public static void main(String[] args) {
        try {
            // Specify the target IP address
            String ipAddress = "192.168.1.1"; // Replace with the IP address you want to check

            // Get the InetAddress for the specified IP address
            InetAddress inetAddress = InetAddress.getByName(ipAddress);

            // Get the current hostname associated with the IP address
            String currentHostname = inetAddress.getHostName();

            System.out.println("Current Hostname for IP " + ipAddress + ": " + currentHostname);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

----------------------------------------------------------------------
how to find the hostname to ip address in code

import java.net.InetAddress;

public class HostnameToIPAddress {
    public static void main(String[] args) {
        try {
            // Specify the hostname you want to resolve to an IP address
            String hostname = "www.example.com"; // Replace with the hostname you want to look up

            // Use InetAddress to resolve the hostname to an array of InetAddress objects
            InetAddress[] addresses = InetAddress.getAllByName(hostname);

            // Loop through the InetAddress objects and print the IP addresses
            for (InetAddress address : addresses) {
                System.out.println("Hostname: " + hostname);
                System.out.println("IP Address: " + address.getHostAddress());
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

-------------------------------------------------------
write a code http class and it's method

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;

public class HttpClass {

    // Method to send an HTTP GET request
    public static String sendHttpGet(String url) throws IOException {
        URL obj = new URL(url);
        HttpURLConnection connection = (HttpURLConnection) obj.openConnection();
        connection.setRequestMethod("GET");

        int responseCode = connection.getResponseCode();
        if (responseCode == HttpURLConnection.HTTP_OK) {
            BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream()));
            String inputLine;
            StringBuilder response = new StringBuilder();

            while ((inputLine = in.readLine()) != null) {
                response.append(inputLine);
            }
            in.close();
            connection.disconnect();
            return response.toString();
        }
        connection.disconnect();
        return null;
    }

    // Method to send an HTTP POST request with data
    public static String sendHttpPost(String url, String postData) throws IOException {
        URL obj = new URL(url);
        HttpURLConnection connection = (HttpURLConnection) obj.openConnection();
        connection.setRequestMethod("POST");
        connection.setDoOutput(true);

        // Send data in the request body
        try (OutputStream os = connection.getOutputStream()) {
            byte[] input = postData.getBytes("UTF-8");
            os.write(input, 0, input.length);
        }

        int responseCode = connection.getResponseCode();
        if (responseCode == HttpURLConnection.HTTP_OK) {
            BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream()));
            String inputLine;
            StringBuilder response = new StringBuilder();

            while ((inputLine = in.readLine()) != null) {
                response.append(inputLine);
            }
            in.close();
            connection.disconnect();
            return response.toString();
        }
        connection.disconnect();
        return null;
    }

    public static void main(String[] args) {
        try {
            String getUrl = "https://jsonplaceholder.typicode.com/posts/1";
            String getResponse = sendHttpGet(getUrl);
            System.out.println("GET Response: " + getResponse);

            String postUrl = "https://jsonplaceholder.typicode.com/posts";
            String postData = "title=foo&body=bar&userId=1";
            String postResponse = sendHttpPost(postUrl, postData);
            System.out.println("POST Response: " + postResponse);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

---------------------------------------------------

write inet address and its method

import java.net.InetAddress;
import java.net.UnknownHostException;

public class InetAddressExample {
    public static void main(String[] args) {
        try {
            // Get InetAddress by host name
            String hostName = "www.example.com";
            InetAddress address = InetAddress.getByName(hostName);

            // Get the IP address
            String ipAddress = address.getHostAddress();
            System.out.println("IP Address for " + hostName + ": " + ipAddress);

            // Get the canonical host name
            String canonicalHostName = address.getCanonicalHostName();
            System.out.println("Canonical Host Name: " + canonicalHostName);

            // Check if it's an IP address
            boolean isIPAddress = InetAddressValidator.isIPAddress(ipAddress);
            System.out.println("Is IP Address: " + isIPAddress);

            // Reverse DNS lookup
            InetAddress reverseAddress = InetAddress.getByName(ipAddress);
            String reverseHostName = reverseAddress.getHostName();
            System.out.println("Reverse DNS Lookup: " + reverseHostName);
        } catch (UnknownHostException e) {
            e.printStackTrace();
        }
    }
}


--------------------------------------------------------------
how to check the port is being used or not

import java.net.Socket;

public class PortChecker {
    public static void main(String[] args) {
        String host = "example.com"; // Replace with the hostname or IP address
        int port = 80; // Replace with the port you want to check

        if (isPortInUse(host, port)) {
            System.out.println("Port " + port + " is in use on " + host);
        } else {
            System.out.println("Port " + port + " is not in use on " + host);
        }
    }

    public static boolean isPortInUse(String host, int port) {
        try (Socket socket = new Socket(host, port)) {
            // If the connection is successful, the port is in use.
            return true;
        } catch (Exception e) {
            // If the connection fails, the port is not in use.
            return false;
        }
    }
}


------------------------------------------------------------
how to create a socket in specif board

import java.net.InetAddress;
import java.net.Socket;

public class SocketOnSpecificInterface {
    public static void main(String[] args) {
        try {
            // Specify the IP address of the network interface
            String interfaceIpAddress = "192.168.0.100"; // Replace with the IP address of your specific board

            // Create an InetAddress object from the interface IP address
            InetAddress interfaceAddress = InetAddress.getByName(interfaceIpAddress);

            // Create a socket bound to the specific interface
            Socket socket = new Socket(interfaceAddress, 0); // You can specify the port if needed

            // Now you can use the socket for communication

            // Don't forget to close the socket when you're done
            socket.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

----------------------------------------------
how to read and download a web page

import java.io.*;
import java.net.HttpURLConnection;
import java.net.URL;

public class WebPageDownloader {
    public static void main(String[] args) {
        String url = "https://www.example.com"; // Replace with the URL of the web page you want to download

        try {
            URL pageUrl = new URL(url);
            HttpURLConnection connection = (HttpURLConnection) pageUrl.openConnection();
            connection.setRequestMethod("GET");

            int responseCode = connection.getResponseCode();

            if (responseCode == HttpURLConnection.HTTP_OK) {
                BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
                String line;
                StringBuilder pageContent = new StringBuilder();

                while ((line = reader.readLine()) != null) {
                    pageContent.append(line);
                }

                reader.close();
                connection.disconnect();

                String content = pageContent.toString();

                // Save the content to a local file
                saveToFile(content, "downloaded_page.html");

                System.out.println("Web page downloaded and saved.");
            } else {
                System.out.println("Failed to download the web page. HTTP response code: " + responseCode);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static void saveToFile(String content, String fileName) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(fileName))) {
            writer.write(content);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
-----------------------------------------------------

how to get connect with the server

import java.io.*;
import java.net.Socket;

public class ClientExample {
    public static void main(String[] args) {
        try {
            String serverAddress = "example.com"; // Replace with the server's IP address or hostname
            int serverPort = 80; // Replace with the server's port

            // Create a socket and connect to the server
            Socket socket = new Socket(serverAddress, serverPort);

            // Create input and output streams for communication
            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

            // Send a message to the server
            out.println("Hello, server!");

            // Receive and display the server's response
            String response = in.readLine();
            System.out.println("Server response: " + response);

            // Close the socket when done
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

---------------------------------------------------
hello world in javafx

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.layout.StackPane;
import javafx.stage.Stage;
import javafx.scene.control.Label;

public class HelloWorldApp extends Application {
    @Override
    public void start(Stage primaryStage) {
        // Create a label with the text "Hello, World!"
        Label label = new Label("Hello, World!");

        // Create a layout to hold the label
        StackPane root = new StackPane();
        root.getChildren().add(label);

        // Create a scene
        Scene scene = new Scene(root, 300, 200);

        // Set the title for the application window
        primaryStage.setTitle("Hello, World in JavaFX");

        // Set the scene for the stage
        primaryStage.setScene(scene);

        // Show the stage
        primaryStage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
--------------------------------------------------
javafx button click event

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.StackPane;
import javafx.stage.Stage;

public class ButtonClickEventExample extends Application {
    public static void main(String[] args) {
        launch(args);
    }

    @Override
    public void start(Stage primaryStage) {
        primaryStage.setTitle("JavaFX Button Click Event Example");

        Button btn = new Button("Click Me"); // Create a button with the label "Click Me"

        // Add a click event handler to the button
        btn.setOnAction(e -> {
            // Define the action to be performed when the button is clicked
            System.out.println("Button clicked!");
        });

        StackPane root = new StackPane();
        root.getChildren().add(btn);

        Scene scene = new Scene(root, 300, 200);

        primaryStage.setScene(scene);
        primaryStage.show();
    }
}

------------------------------------------------
javafx list view

import javafx.application.Application;
import javafx.collections.FXCollections;
import javafx.collections.ObservableList;
import javafx.scene.Scene;
import javafx.scene.control.ListView;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

public class ListViewExample extends Application {
    @Override
    public void start(Stage primaryStage) {
        primaryStage.setTitle("JavaFX ListView Example");

        // Create a list of items to display in the ListView
        ObservableList<String> items = FXCollections.observableArrayList(
            "Item 1", "Item 2", "Item 3", "Item 4", "Item 5"
        );

        // Create the ListView and set its items
        ListView<String> listView = new ListView<>(items);

        // Add an event handler to respond to item selection
        listView.getSelectionModel().selectedItemProperty().addListener((observable, oldValue, newValue) -> {
            System.out.println("Selected item: " + newValue);
        });

        VBox vbox = new VBox(listView);
        Scene scene = new Scene(vbox, 300, 200);
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}

---------------------------------------------------
strunt hello world

create a strunt action class 

package com.example;

import org.apache.struts.action.Action;
import org.apache.struts.action.ActionForm;
import org.apache.struts.action.ActionForward;
import org.apache.struts.action.ActionMapping;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class HelloWorldAction extends Action {
    public ActionForward execute(ActionMapping mapping, ActionForm form,
            HttpServletRequest request, HttpServletResponse response)
            throws Exception {
        return mapping.findForward("success");
    }
}

create a jsp view 

<%@ page contentType="text/html; charset=UTF-8" %>
<%@ taglib uri="http://struts.apache.org/tags-html" prefix="html" %>
<html>
<head>
    <title>Hello, World!</title>
</head>
<body>
    <h1>Hello, World!</h1>
</body>
</html>

web.xml 

<filter>
    <filter-name>action</filter-name>
    <filter-class>org.apache.struts2.dispatcher.filter.StrutsPrepareAndExecuteFilter</filter-class>
</filter>

<filter-mapping>
    <filter-name>action</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>

---------------------------------------------------------
srunts file handling

create a form been

package com.example.form;

import org.apache.struts.action.ActionForm;

public class MyForm extends ActionForm {
    private String firstName;
    private String lastName;

    // Getter and setter methods for the form fields
    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }
}

create an action class 

package com.example;

import com.example.form.MyForm;
import org.apache.struts.action.Action;
import org.apache.struts.action.ActionForm;
import org.apache.struts.action.ActionForward;
import org.apache.struts.action.ActionMapping;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class FormHandlingAction extends Action {
    public ActionForward execute(ActionMapping mapping, ActionForm form,
            HttpServletRequest request, HttpServletResponse response)
            throws Exception {
        MyForm myForm = (MyForm) form;

        // Get form data
        String firstName = myForm.getFirstName();
        String lastName = myForm.getLastName();

        // Perform data processing or validation here

        // Return a response (forward to a JSP page)
        return mapping.findForward("success");
    }
}


create jsp page

<%@ page contentType="text/html; charset=UTF-8" %>
<%@ taglib uri="http://struts.apache.org/tags-html" prefix="html" %>

<html>
<head>
    <title>Form Handling</title>
</head>
<body>
    <html:form action="/formHandling">
        <html:text property="firstName" /> <br>
        <html:text property="lastName" /> <br>
        <html:submit />
    </html:form>
</body>
</html>


xml file 

<form-beans>
    <form-bean name="myForm" type="com.example.form.MyForm" />
</form-beans>

<action-mappings>
    <action path="/formHandling" type="com.example.FormHandlingAction" name="myForm"
        scope="request" input="/form.jsp">
        <forward name="success" path="/success.jsp" />
    </action>
</action-mappings>

------------------------------------------------------------------


