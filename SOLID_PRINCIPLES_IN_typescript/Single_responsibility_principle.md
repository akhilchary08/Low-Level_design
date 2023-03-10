**Single Responsibility Principle**: 
This principle states that “**a class should have only one reason to change**” which means every class should have a single responsibility or single job or single purpose.
example-1:

    class  Student  {  
	    public createStudentAccount(){  
	    // some logic  
	    }  
	    public calculateStudentGrade(){  
	    // some logic  
	    }  
	    public generateStudentData(){  
	    // some logic  
	    }  
    }
To pinpoint a reason to change, we need to look into what our program’s responsibilities are. We might change the `Student` class for three different reasons:

-   The `createStudentAccount` computation logic changes
-   The logic for calculating student grades changes
-   The format of generating and reporting student data changes
Hence, the single responsibility principle is broken.

	    class  StudentAccount {
			public  createStudentAccount() {
				//some logic
			}
		}
		class  StudentGrade {
			public  calculateStudentGrade() {
			}
		} 
		class  StudentData {
			public  generateStudentData() {
			}
		}

Now that we‘ve divided the classes, each has only one duty, one responsibility, and only one alteration that needs to be made. Now, our code is simpler to explain and comprehend.
