# Overview  
This repository is for tracking development and learning related to validation in Spring MVC.  

## Notes

1. **@NotNull, @Size and @Valid**  
    **@NotNull**: Annotation to make sure the field is always set and is not a null value.  
    **@Size**: Annotation to make sure the field when present has at least a minimum set of characters.  
    **@Valid**: Annotation prefixed to the binding object parameter passed to the controller function 
        to make sure all constraints are satisfied.  
    ```java
    public class Customer {
        // ...
        @NotNull(message = "is required")
        @Size(min = 1, message = "is required")
        private String lastName;
        // ...
    }  
    ```
    ```java
    @Controller
    public class CustomerController {
        // ...
        @PostMapping("/processForm")
        public String processForm(@Valid @ModelAttribute("customer") Customer customer, BindingResult result) {
            if(result.hasErrors()) {
                return "customer-form";
            } else {
                return "customer-confirmation";
            }
        }
        // ...
    }
    ```