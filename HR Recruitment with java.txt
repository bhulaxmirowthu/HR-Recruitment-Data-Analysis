package Bujji;
import java.io.*;
import java.util.*;
public class Hrproject {
	
  public static void main(String[] args) {

	        String filePath = "hr_data.csv";

	        List<String[]> data = new ArrayList<>();

	        try {
	            BufferedReader br = new BufferedReader(new FileReader(filePath));
	            String line;

	            while ((line = br.readLine()) != null) {
	                String[] values = line.split(",");
	                data.add(values);
	            }
	            br.close();

	        } catch (Exception e) {
	            System.out.println("Error reading file: " + e.getMessage());
	            return;
	        }

	        // Variables for analysis
	        int total = 0;
	        int selected = 0;
	        int rejected = 0;
	        double totalSalary = 0;
	        int salaryCount = 0;

	        Map<String, Integer> deptCount = new HashMap<>();

	        // Start from 1 to skip header
	        for (int i = 1; i < data.size(); i++) {

	            total++;

	            String department = data.get(i)[6];
	            String status = data.get(i)[7];

	            // Department count
	            deptCount.put(department, deptCount.getOrDefault(department, 0) + 1);

	            if (status.equalsIgnoreCase("Selected")) {
	                selected++;
	                totalSalary += Double.parseDouble(data.get(i)[8]);
	                salaryCount++;
	            } else {
	                rejected++;
	            }
	        }

	        // OUTPUT SECTION
	        System.out.println("===== HR RECRUITMENT ANALYSIS =====");

	        System.out.println("Total Candidates: " + total);
	        System.out.println("Selected: " + selected);
	        System.out.println("Rejected: " + rejected);

	        System.out.println("\n----- Department Wise Applications -----");
	        for (String dept : deptCount.keySet()) {
	            System.out.println(dept + " : " + deptCount.get(dept));
	        }

	        if (salaryCount > 0) {
	            System.out.println("\nAverage Salary Offered: " + (totalSalary / salaryCount));
	        }

	        System.out.println("=======================================");
	    }
	}


	
