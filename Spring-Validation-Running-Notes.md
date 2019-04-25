## BindingResult
1. This is part of spring's validation package.
2. This has to follow the object that is being validated otherwise this wont work.
3. That is, in the method param, this has to be exactly after the object (with a @Valid) annot.
4. This acts as a data binder holding the results of the validations performed.
5. If you dont put this after the model being validated then you will get this error:
'An Errors/BindingResult argument is expected to be declared immediately after the model attribute'
6. And, if you don't use this at all, then the validation happens but binding the result of the validation will happen and that will throw an error.
7. Bindingresult also has methods like reject (for global errors - not related to one field but related to the whole object) and rejectValue (with an option to pass custom error message) - basically this acts the validation result holder and passes the data to the view for it to render

## ValidationMessages.properties
1. This is the property file which hibernate (or any jpa provider for that matter) will look for when providing error messages for the validations done using jpa validation annot.
2. So to override the default error messages, you can use the message attr. of the jpa validation annot. and provide a corresponding custom error message in a custom ValidationMessages.properties file.

## @Validated
1. This is part of spring validation package.
2. Use this to annotate the class/object that is being validated using spring validator.
3. As soon as the Spring Controller sees this annot. against an object, it's respective validator (which is set using the webdatabinder annotated w/ @InitBinder) will be called.
4. If you dont use this annot. then the respective Validator will never be called.
5. For instance, if there is a Model M and it has a validator MValidator (which implements Validator interface), then in the controller method (the method which gets called from the UI) the method param of the object M should have a prefix of @Validated annot. for it's validator (MValidator) to be invoked.

## Bean validation vs Spring validator
1. Bean validation means using the javax annot. on the bean fields such as @NotEmpty, @NotNull, @Size etc. which are then automatically validated by the jpa provider (hibernate - using hibernate validator).
2. When you use Spring validator you do not use those javax annot. and rather create a separate class for by implementing the Validator interface and override it's supports and validate methods.
3. Spring validator gives you more control for complex validations such as applying some logic on the validation like age<10 and age>20 or in the range of x to x, something like that.
4. If you use Spring validator, use @Validated otherwise @Valid in the controller.
5. For Spring Validator, you need to DI it's instance in the controller.
6. Spring Validator also binds its errors to the BindingResult class.
7. Both these are not mutually exclusive, so can be used together.
8. But, both of these are only for UI level validations i.e. to perform validations on what user has entered on the screen, not for other business logic.

