
## Relationships
1. Bi-dir 1-1<br/>
   a. Example: Two entities - Employee and Cubicle.<br/>
   b. Entity Employee references a single instance of Entity Cubicle.<br/>
   c. Entity Cubicle references a single instance of Entity Employee.<br/>
   d. Employee is the owner of this rel.<br/>
   e. Employee is mapped to table EMPLOYEE.<br/>
   f. Cubicle is mapped to table CUBICLE.<br/>
   g. EMPLOYEE tab contains a fk to CUBICLE.<br/>
2. Bi-dir *-1/1-* <br/>
   a. Example:Two entities - Employee and Department .<br/>
   b. Entity Employee references a single instance of Entity Department.<br/>
   c. Entity Department references a collection of Entity Employee.<br/>
   d. Entity Employee is the owner of the relationship.   <br/>
   e. Employee is mapped to table EMPLOYEE.<br/>
   f. Department is mapped to tab. DEPARTMENT.<br/>
   g. EMPLOYEE tab contains a fk of DEPARTMENT.<br/>
3. Uni-dir 1-1<br/>
   a. Example: Two entities: Employee and TravelProfile<br/>
   b. Entity Employee references a single instance of Entity TravelProfile.<br/>
   c. Entity TravelProfile does not reference Entity Employee.<br/>
   d. Employee is the owner of this rel.<br/>
   e. Employee is mapped to tab EMPLOYEE.<br/>
   f. TravelProfile is mapped to tab TRAVELPROFILE.<br/>
   g. EMPLOYEE tab has a fk to TRAVELPROFILE.<br/>
4. Uni-dir *-1 <br/>
   a. Example: Two entities: Employee and Address.<br/>
   b. Entity Employee references a single instance of Entity Address.<br/>
   c. Entity Address does not reference Entity Employee.<br/>
   d. Entity Employee is the owner of the relationship.<br/>
   e. Employee is mapped to tab EMPLOYEE.<br/>
   f. Address is mapped to tab ADDRESS.<br/>
   g. EMPLOYEE contains a fk to ADDRESS.<br/>
5. Bi-dir *-* <br/>
   a. Example: Two entities: Project and Employee.<br/>
   b. Entity Project references a collection of Entity Employee.<br/>
   c. Entity Employee references a collection of Entity Project.<br/>
   d. Entity Project is the owner of the relationship.<br/>
   e. Project is mapped to tab PROJECT.<br/>
   f. Employee is mapped to tab EMPLOYEE.<br/>
   g. Join table PROJECT_EMPLOYEE has two fk cols each belonging to PROJECT and EMPLOYEE.<br/>
6. Uni-dir 1-* <br/>
   a. Example: Two entities: Employee and AnnualReview.<br/>
   b. Entity Employee references a collection of Entity AnnualReview.<br/>
   c. Entity AnnualReview does not reference Entity Employee.<br/>
   d. Entity Employee is the owner of the relationship.<br/>
   e. Employee is mapped to tab EMPLOYEE.<br/>
   f. AnnualReview is mapped to tab ANNUALREVIEW.<br/>
   g. Join tab. EMPLOYEE_ANNUALREVIEW has 2 fk cols each belonging to EMPLOYEE and ANNUALREVIEW.<br/>
7. Uni-dir *-* <br/>
   a. Example: Two entities: Employee and Patent.<br/>
   b. Entity Employee references a collection of Entity Patent.<br/>
   c. Entity Patent does not reference Entity Employee.<br/>
   d. Entity Employee is the owner of the relationship.<br/>
   e. Employee is mapped to tab EMPLOYEE.<br/>
   f. Patent is mapped to tab PATENT.<br/>
   g. Join tab EMPLOYEE_PATENT has 2 fk cols each belonging to EMPLOYEE and PATENT.<br/>
