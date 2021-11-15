import React,{useState,useEffect} from "react";

const StudentRegistration = () => {
    const initialValues = {username:"",email:"",rollnumber:"",division:""}; 
    const [formValues,setFormValues] = useState(initialValues);
    const [formErrors,setFormErrors] = useState({});
    const [isSubmit,setIsSubmit] = useState(false);

    const handelChange = (e) =>
    {
        const {name, value} = e.target;
        setFormValues({...formValues, [name]: value });
        setIsSubmit(true);
    }

    const handelSubmit = (e) =>
    {
        e.preventDefault();
        setFormErrors(validate(formValues));
    }

    useEffect(() => {
        console.log(formErrors);
        if(Object.keys(formErrors).length === 0 && isSubmit){
            console.log(formValues);
        }
    },[formErrors])

    const validate = (values) => 
    {
        const errors = {};
        const mailformat = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if(!values.username)
        {
            errors.username = "Username is required.";
        }
        if(!values.email)
        {
            errors.email = "Email is required.";
        }
        else if(!mailformat.test(values.email))
        {
            errors.email ="This is not valid email."
        }
        if(!values.rollnumber)
        {
            errors.rollnumber = "Rollnumber is required.";
        }
        if(!values.division)
        {
            errors.division = "Division is required.";
        }
        return errors;
    }

    return ( 
        <>
            {Object.keys(formErrors).length === 0 && isSubmit ? (
                <div className="successMessage">Success</div>
            ) : (
                <pre>{JSON.stringify(formValues,undefined,2)}</pre>
            )}
            
            <form onSubmit={handelSubmit}>
            <h1>Registration Form</h1>
            <div className="ui divider"></div>
            <div className="ui form">
                <div className="form-group">
                    <label>Username</label>
                    <input
                        type="text"
                        class="form-control"
                        name="username"
                        value={formValues.username}
                        placeholder="Username"
                        onChange={handelChange}
                    />
                </div>
                <p className="error">{formErrors.username}</p>
                <div className="form-group">
                    <label>Email</label>
                    <input
                        type="text"
                        class="form-control"
                        name="email"
                        value={formValues.email}
                        placeholder="Email"
                        onChange={handelChange}
                    />
                </div>
                <p className="error">{formErrors.email}</p>
                <div className="form-group">
                    <label>Roll Number</label>
                    <input
                        type="text"
                        class="form-control"
                        name="rollnumber"
                        value={formValues.rollnumber}
                        placeholder="Roll number"
                        onChange={handelChange}
                    />
                </div>
                <p className="error">{formErrors.rollnumber}</p>
                <div className="form-group">
                    <label>Division</label>
                    <input
                        type="text"
                        class="form-control"
                        name="division"
                        value={formValues.division}
                        placeholder="Division"
                        onChange={handelChange}
                    />
                </div>
                <p className="error">{formErrors.division}</p>
                <button className="fluid ui button blue">Submit</button>
            </div>
            </form>
        </>
    );
};

export {StudentRegistration};
