import { useState } from "react";
import { BiFingerprint } from "react-icons/bi";

const Card = ({ children }) => <div className='border rounded-lg p-4 shadow-md'>{children}</div>;
const Input = ({ name, type = 'text', placeholder, onChange }) => (
  <input name={name} type={type} placeholder={placeholder} onChange={onChange} className='border p-2 w-full rounded mb-2' />
);
const Button = ({ children, onClick }) => (
  <button onClick={onClick} className='bg-blue-500 text-white p-2 rounded w-full'>{children}</button>
);
const useToast = () => ({
  toast: ({ title, description }) => alert(`${title}: ${description}`),
});

export default function TenantApplicationPrototype() {
  const { toast } = useToast();
  const [tenantData, setTenantData] = useState({
    name: "",
    email: "",
    phone: "",
    studentId: "",
    property: "",
    tenantHomeAddress: "",
    universityCourse: "",
    universityYear: "",
    passportNumber: "",
    rightToRentCode: "",
    dateOfBirth: "",
    hasUkGuarantor: "",
    guarantorName: "",
    guarantorEmail: "",
    guarantorPhone: "",
    guarantorAddress: ""
  });

  const handleChange = (e) => {
    setTenantData({ ...tenantData, [e.target.name]: e.target.value });
  };

  const handleSubmit = () => {
    toast({
      title: "Application Submitted",
      description: `Application for ${tenantData.property} submitted by ${tenantData.name}`,
    });
  };

  return (
    <div className="flex flex-col items-center gap-4 p-6">
      <Card>
        <h2 className="text-xl font-bold mb-4">Tenant Application</h2>
        <Input name="name" placeholder="Full Name" onChange={handleChange} />
        <Input name="email" type="email" placeholder="Email Address" onChange={handleChange} />
        <Input name="phone" type="tel" placeholder="Phone Number" onChange={handleChange} />
        <Input name="studentId" placeholder="Student ID" onChange={handleChange} />
        <Input name="property" placeholder="Property Applied For" onChange={handleChange} />
        <Input name="tenantHomeAddress" placeholder="Tenant's Home Address" onChange={handleChange} />
        <Input name="universityCourse" placeholder="University Course" onChange={handleChange} />
        <Input name="universityYear" placeholder="University Year (e.g. Second Year)" onChange={handleChange} />
        <Input name="passportNumber" placeholder="Passport Number" onChange={handleChange} />
        <Input name="rightToRentCode" placeholder="Right to Rent Share Code" onChange={handleChange} />
        <a href="https://www.gov.uk/view-right-to-rent" target="_blank" className="text-blue-500 underline">Check Right to Rent</a>
        <Input name="dateOfBirth" type="date" placeholder="Date of Birth" onChange={handleChange} />
        <label className="block mb-2">Do you have a UK-based Guarantor?</label>
        <Input name="hasUkGuarantor" type="radio" value="yes" onChange={handleChange} /> Yes
        <Input name="hasUkGuarantor" type="radio" value="no" onChange={handleChange} /> No
        <Input name="guarantorName" placeholder="Guarantor's Full Name" onChange={handleChange} />
        <Input name="guarantorEmail" type="email" placeholder="Guarantor's Email Address" onChange={handleChange} />
        <Input name="guarantorPhone" type="tel" placeholder="Guarantor's Phone Number" onChange={handleChange} />
        <Input name="guarantorAddress" placeholder="Guarantor's Address" onChange={handleChange} />
        <Button onClick={handleSubmit}>Submit Application</Button>
      </Card>

      <Card>
        <h2 className="text-xl font-bold mb-4">Admin Login</h2>
        <Input name="adminEmail" type="email" placeholder="Admin Email" />
        <Input name="password" type="password" placeholder="Password" />
        <Button>Login</Button>
        <Button>
          <BiFingerprint size={20} /> Use Biometric Login
        </Button>
      </Card>
    </div>
  );
}
