
## Relationships
1. Bi-dir 1-1<br/>
   a. Example: Two entities - Employee and Cubicle.<br/>
   b. Entity Employee references a single instance of Entity Cubicle.<br/>
   c. Entity Cubicle references a single instance of Entity Employee.<br/>
   d. Employee is the owner of this rel.<br/>
   e. Employee is mapped to table EMPLOYEE.<br/>
   f. Cubicle is mapped to table CUBICLE.<br/>
   g. EMPLOYEE tab contains a fk to CUBICLE.<br/>
2. Bi-dir *-1/1-*<br/>
   a. Example:Two entities - Employee and Department .<br/>
   b. Entity Employee references a single instance of Entity Department.
   c. Entity Department references a collection of Entity Employee.
   d. Entity Employee is the owner of the relationship.   
   e. Employee is mapped to table EMPLOYEE.
   f. Department is mapped to tab. DEPARTMENT.
   g. EMPLOYEE tab contains a fk of DEPARTMENT.
3. Uni-dir 1-1
   a. Example: Two entities: Employee and TravelProfile
   b. Entity Employee references a single instance of Entity TravelProfile.
   c. Entity TravelProfile does not reference Entity Employee.
   d. Employee is the owner of this rel.
   e. Employee is mapped to tab EMPLOYEE.
   f. TravelProfile is mapped to tab TRAVELPROFILE.
   g. EMPLOYEE tab has a fk to TRAVELPROFILE.
4. Uni-dir *-1
   a. Example: Two entities: Employee and Address.
   b. Entity Employee references a single instance of Entity Address.
   c. Entity Address does not reference Entity Employee.
   d. Entity Employee is the owner of the relationship.
   e. Employee is mapped to tab EMPLOYEE.
   f. Address is mapped to tab ADDRESS.
   g. EMPLOYEE contains a fk to ADDRESS.
5. Bi-dir *-*
   a. Example: Two entities: Project and Employee.
   b. Entity Project references a collection of Entity Employee.
   c. Entity Employee references a collection of Entity Project.
   d. Entity Project is the owner of the relationship.
   e. Project is mapped to tab PROJECT.
   f. Employee is mapped to tab EMPLOYEE.
   g. Join table PROJECT_EMPLOYEE has two fk cols each belonging to PROJECT and EMPLOYEE.
6. Uni-dir 1-*
   a. Example: Two entities: Employee and AnnualReview.
   b. Entity Employee references a collection of Entity AnnualReview.
   c. Entity AnnualReview does not reference Entity Employee.
   d. Entity Employee is the owner of the relationship.
   e. Employee is mapped to tab EMPLOYEE.
   f. AnnualReview is mapped to tab ANNUALREVIEW.
   g. Join tab. EMPLOYEE_ANNUALREVIEW has 2 fk cols each belonging to EMPLOYEE and ANNUALREVIEW.
7. Uni-dir *-*
   a. Example: Two entities: Employee and Patent.
   b. Entity Employee references a collection of Entity Patent.
   c. Entity Patent does not reference Entity Employee.
   d. Entity Employee is the owner of the relationship.
   e. Employee is mapped to tab EMPLOYEE.
   f. Patent is mapped to tab PATENT.
   g. Join tab EMPLOYEE_PATENT has 2 fk cols each belonging to EMPLOYEE and PATENT.
