import { useState, useEffect, useRef } from "react";

// ─── SCHEME DATABASE ───────────────────────────────────────────────
const SCHEMES = [
  { id:1, name:"NSP Post-Matric Scholarship (SC Students)", category:"Scholarship", icon:"🎓",
    benefit:"₹3,500–₹23,400/year", deadline:"2024-10-31", state:"All India",
    minAge:0, maxAge:99, gender:"all", incomeMax:250000, categories:["SC"],
    description:"Central govt scholarship for SC students in post-matric education. Covers maintenance & tuition fees.",
    rules:["Category must be SC","Annual family income below ₹2.5 Lakh","Must be pursuing post-matric education"],
    applyLink:"https://scholarships.gov.in", source:"National Scholarship Portal", ministry:"Ministry of Social Justice", tag:"Central Govt",
    documents:["Caste Certificate","Income Certificate","Marksheet","Bank Passbook","Aadhaar Card"] },
  { id:2, name:"NSP Pre-Matric Scholarship (OBC Students)", category:"Scholarship", icon:"📚",
    benefit:"₹500–₹7,000/year", deadline:"2024-10-31", state:"All India",
    minAge:0, maxAge:20, gender:"all", incomeMax:100000, categories:["OBC"],
    description:"Scholarship for OBC students studying in Class IX and X. Covers books, uniform and fees.",
    rules:["Category must be OBC","Annual family income below ₹1 Lakh","Studying in Class IX or X","Age below 20"],
    applyLink:"https://scholarships.gov.in", source:"National Scholarship Portal", ministry:"Ministry of Minority Affairs", tag:"Central Govt",
    documents:["OBC Certificate","Income Certificate","School ID","Aadhaar Card"] },
  { id:3, name:"PM Yasasvi Scholarship Scheme", category:"Scholarship", icon:"⭐",
    benefit:"₹75,000–₹1,25,000/year", deadline:"2024-11-30", state:"All India",
    minAge:13, maxAge:30, gender:"all", incomeMax:250000, categories:["OBC","EWS"],
    description:"High-value scholarship for OBC/EWS/DNT students in top schools and colleges. One of India's richest merit scholarships.",
    rules:["Category: OBC, EWS or DNT","Annual family income below ₹2.5 Lakh","Age 13–30","Must clear YASASVI entrance test"],
    applyLink:"https://yet.nta.ac.in", source:"NTA / NSP", ministry:"Ministry of Social Justice", tag:"Central Govt",
    documents:["Category Certificate","Income Certificate","Marksheet (Class 8 or 10)","Aadhaar Card"] },
  { id:4, name:"Pradhan Mantri Awas Yojana (Urban)", category:"Housing", icon:"🏠",
    benefit:"Up to ₹2.67 Lakh subsidy", deadline:"Ongoing", state:"All India",
    minAge:18, maxAge:99, gender:"all", incomeMax:1800000, categories:["General","OBC","SC","ST","EWS"],
    description:"Credit-linked subsidy for first-time home buyers in urban areas. Applicable for EWS/LIG/MIG categories.",
    rules:["Must not own a pucca house anywhere in India","Annual income below ₹18 Lakh (MIG-II)","First-time home buyer"],
    applyLink:"https://pmaymis.gov.in", source:"Ministry of Housing & Urban Affairs", ministry:"MoHUA", tag:"Central Govt",
    documents:["Aadhaar Card","Income Proof","Property Documents","Bank Statement"] },
  { id:5, name:"Ayushman Bharat PM-JAY", category:"Healthcare", icon:"🏥",
    benefit:"₹5 Lakh health cover/year (per family)", deadline:"Ongoing", state:"All India",
    minAge:0, maxAge:99, gender:"all", incomeMax:200000, categories:["General","OBC","SC","ST","EWS"],
    description:"World's largest govt health insurance. Covers secondary and tertiary hospitalization for 10 crore+ families.",
    rules:["Listed in SECC-2011 database or deprived categories","Income below ₹2 Lakh/year","No existing govt health insurance"],
    applyLink:"https://pmjay.gov.in", source:"National Health Authority", ministry:"Ministry of Health", tag:"Central Govt",
    documents:["Aadhaar Card","Ration Card","Income Certificate"] },
  { id:6, name:"PM Kisan Samman Nidhi", category:"Farmer", icon:"🌾",
    benefit:"₹6,000/year (3 installments)", deadline:"Ongoing", state:"All India",
    minAge:18, maxAge:99, gender:"all", incomeMax:9999999, categories:["General","OBC","SC","ST","EWS"],
    description:"Direct income support of ₹6,000/year to small and marginal farmer families through DBT.",
    rules:["Must be a land-holding farmer","Should not be an income taxpayer","Land records must be updated"],
    applyLink:"https://pmkisan.gov.in", source:"PM-Kisan Portal", ministry:"Ministry of Agriculture", tag:"Central Govt",
    documents:["Khasra/Khatauni (land record)","Aadhaar Card","Bank Passbook"] },
  { id:7, name:"Post Matric Scholarship for ST Students", category:"Scholarship", icon:"🎓",
    benefit:"₹3,000–₹14,800/year", deadline:"2024-10-31", state:"All India",
    minAge:0, maxAge:35, gender:"all", incomeMax:250000, categories:["ST"],
    description:"Scholarship for ST students from Class XI onwards. Covers tuition, maintenance and special allowances.",
    rules:["Category must be ST","Annual family income below ₹2.5 Lakh","Pursuing education from Class XI onward"],
    applyLink:"https://scholarships.gov.in", source:"National Scholarship Portal", ministry:"Ministry of Tribal Affairs", tag:"Central Govt",
    documents:["Tribe Certificate","Income Certificate","Previous Marksheet","Aadhaar Card"] },
  { id:8, name:"Central Sector Scheme – Top Class Education (SC)", category:"Scholarship", icon:"🏛️",
    benefit:"₹2 Lakh/year (tuition + maintenance)", deadline:"2024-09-30", state:"All India",
    minAge:17, maxAge:35, gender:"all", incomeMax:600000, categories:["SC"],
    description:"Premium scholarship for SC students admitted to IITs, NITs, IIMs, AIIMS and other top institutions.",
    rules:["Category must be SC","Family income below ₹6 Lakh","Admitted to notified premier institutions","Fresh admissions only"],
    applyLink:"https://scholarships.gov.in", source:"National Scholarship Portal", ministry:"Ministry of Social Justice", tag:"Central Govt",
    documents:["SC Certificate","Income Certificate","Admission Letter (IIT/NIT/AIIMS etc.)","Aadhaar Card"] },
  { id:9, name:"Vidyadhan Scholarship (Buddy4Study)", category:"Scholarship", icon:"💡",
    benefit:"₹10,000–₹75,000/year", deadline:"2024-12-31", state:"All India",
    minAge:15, maxAge:30, gender:"all", incomeMax:200000, categories:["General","OBC","SC","ST","EWS"],
    description:"Merit-cum-means scholarship for motivated students from low-income families to complete higher education.",
    rules:["Annual family income below ₹2 Lakh","Age 15–30","Good academic record (60%+)","Enrolled in recognized institution"],
    applyLink:"https://www.buddy4study.com/scholarship/vidyadhan", source:"Buddy4Study", ministry:"Sarojini Damodaran Foundation", tag:"Private NGO",
    documents:["Income Certificate","Marksheet","Institution ID","Aadhaar Card"] },
  { id:10, name:"Sukanya Samriddhi Yojana", category:"Girl Child", icon:"👧",
    benefit:"7.6% interest (tax-free maturity)", deadline:"Ongoing", state:"All India",
    minAge:0, maxAge:10, gender:"female", incomeMax:9999999, categories:["General","OBC","SC","ST","EWS"],
    description:"Small savings scheme for the girl child's education and marriage. Account can be opened for girls up to age 10.",
    rules:["Girl child below age 10","Indian resident","Max 2 accounts per family"],
    applyLink:"https://www.indiapost.gov.in", source:"India Post / Banks", ministry:"Ministry of Finance", tag:"Central Govt",
    documents:["Birth Certificate of girl","Parent Aadhaar","Parent PAN Card"] },
  { id:11, name:"NMMS – National Means-cum-Merit Scholarship", category:"Scholarship", icon:"📝",
    benefit:"₹12,000/year", deadline:"2024-11-15", state:"All India",
    minAge:12, maxAge:18, gender:"all", incomeMax:150000, categories:["General","OBC","SC","ST","EWS"],
    description:"Central scholarship for Class IX-XII students from weaker economic sections with strong academic record.",
    rules:["Annual family income below ₹1.5 Lakh","Age 12–18","Studying in Class IX (at application time)","Minimum 55% in Class VIII"],
    applyLink:"https://scholarships.gov.in", source:"National Scholarship Portal", ministry:"Ministry of Education", tag:"Central Govt",
    documents:["Income Certificate","Class VIII Marksheet","School Certificate","Aadhaar Card"] },
  { id:12, name:"Beti Bachao Beti Padhao", category:"Girl Child", icon:"🌸",
    benefit:"Multiple benefits via linked govt programs", deadline:"Ongoing", state:"All India",
    minAge:0, maxAge:18, gender:"female", incomeMax:9999999, categories:["General","OBC","SC","ST","EWS"],
    description:"Umbrella scheme for welfare of girl child – education incentives, healthcare access, and awareness programs.",
    rules:["Girl child","Age below 18","Indian resident"],
    applyLink:"https://wcd.nic.in/bbbp-schemes", source:"Ministry of WCD", ministry:"Ministry of Women & Child Development", tag:"Central Govt",
    documents:["Birth Certificate","Aadhaar Card","Parent ID Proof"] },
  { id:13, name:"Inspire Scholarship (SHE)", category:"Scholarship", icon:"🔬",
    benefit:"₹80,000/year for 5 years", deadline:"2024-12-15", state:"All India",
    minAge:17, maxAge:22, gender:"all", incomeMax:9999999, categories:["General","OBC","SC","ST","EWS"],
    description:"Scholarship for students pursuing BSc/BS/Int MSc in Natural & Basic Sciences. Promotes research culture in India.",
    rules:["Pursuing BSc/BS in Natural Sciences (Physics, Chemistry, Biology, Maths etc.)","Top 1% in Class XII board exams","Age 17–22"],
    applyLink:"https://online-inspire.gov.in", source:"DST INSPIRE Portal", ministry:"Dept. of Science & Technology", tag:"Central Govt",
    documents:["Class XII Marksheet (top 1% proof)","Institution Admission Letter","Aadhaar Card"] },
  { id:14, name:"Pragati Scholarship (AICTE) – Girls", category:"Scholarship", icon:"👩‍💻",
    benefit:"₹50,000/year + ₹2,000 contingency", deadline:"2024-12-31", state:"All India",
    minAge:0, maxAge:30, gender:"female", incomeMax:800000, categories:["General","OBC","SC","ST","EWS"],
    description:"Scholarship for girl students in AICTE-approved technical institutions. Promotes women in engineering and technology.",
    rules:["Gender: Female only","Enrolled in AICTE-approved degree/diploma","Family income below ₹8 Lakh","First year or lateral entry"],
    applyLink:"https://www.aicte-india.org/bureaus/bos/pragati-saksham", source:"AICTE", ministry:"Ministry of Education", tag:"Central Govt",
    documents:["Aadhaar Card","Income Certificate","AICTE Institution Admission Letter","Previous Marksheet"] },
];

function checkEligibility(scheme, profile) {
  if (!profile.age && !profile.income) return { status:"unknown", reasons:[], score:0 };
  const age = parseInt(profile.age) || 0;
  const income = parseInt(profile.income) || 0;
  const reasons = [];
  let passed = 0; let total = 0;

  // Age
  total++;
  if (age >= scheme.minAge && age <= scheme.maxAge) {
    passed++; reasons.push({ pass:true, text:`Age ${age} is within the required range (${scheme.minAge}–${scheme.maxAge} yrs)` });
  } else {
    reasons.push({ pass:false, text:`Age ${age} is outside the allowed range (${scheme.minAge}–${scheme.maxAge} yrs)` });
  }
  // Income
  total++;
  if (income <= scheme.incomeMax) {
    passed++; reasons.push({ pass:true, text:`Family income ₹${income.toLocaleString()} is within the ₹${scheme.incomeMax.toLocaleString()} limit` });
  } else {
    reasons.push({ pass:false, text:`Family income ₹${income.toLocaleString()} exceeds the limit of ₹${scheme.incomeMax.toLocaleString()}` });
  }
  // Gender
  if (scheme.gender !== "all") {
    total++;
    if (profile.gender === scheme.gender) {
      passed++; reasons.push({ pass:true, text:`Gender eligibility met (${scheme.gender} only)` });
    } else {
      reasons.push({ pass:false, text:`This scheme is for ${scheme.gender} applicants only` });
    }
  }
  // Category
  if (scheme.categories.length < 5) {
    total++;
    const cats = Array.isArray(scheme.categories) ? scheme.categories : [scheme.categories];
    if (cats.includes(profile.category)) {
      passed++; reasons.push({ pass:true, text:`Category '${profile.category}' is eligible for this scheme` });
    } else {
      reasons.push({ pass:false, text:`Category '${profile.category || "not set"}' not eligible. Required: ${cats.join(", ")}` });
    }
  }
  const matchScore = total > 0 ? Math.round((passed/total)*100) : 0;
  const status = passed === total ? "eligible" : passed >= total*0.6 ? "partial" : "not_eligible";
  return { status, reasons, score:matchScore };
}

const INCOME_OPTIONS = [
  { label:"Below ₹50,000", value:40000 },
  { label:"₹50,001 – ₹1 Lakh", value:75000 },
  { label:"₹1 Lakh – ₹1.5 Lakh", value:125000 },
  { label:"₹1.5 Lakh – ₹2.5 Lakh", value:200000 },
  { label:"₹2.5 Lakh – ₹5 Lakh", value:375000 },
  { label:"₹5 Lakh – ₹8 Lakh", value:650000 },
  { label:"₹8 Lakh – ₹12 Lakh", value:1000000 },
  { label:"Above ₹12 Lakh", value:1500000 },
];

const CATEGORY_COLORS = {
  Scholarship: { light:"#EFF6FF", accent:"#2563EB", border:"#BFDBFE", tag:"#1D4ED8" },
  Healthcare:  { light:"#F0FDF4", accent:"#16A34A", border:"#BBF7D0", tag:"#15803D" },
  Housing:     { light:"#FFFBEB", accent:"#D97706", border:"#FDE68A", tag:"#B45309" },
  Farmer:      { light:"#F0FDF4", accent:"#15803D", border:"#A7F3D0", tag:"#065F46" },
  "Girl Child":{ light:"#FDF2F8", accent:"#DB2777", border:"#FBCFE8", tag:"#9D174D" },
};

// ─── MAIN APP ─────────────────────────────────────────────────────
export default function App() {
  const [page, setPage] = useState("landing");
  const [user, setUser] = useState(null);
  const [profile, setProfile] = useState({});
  const [loginData, setLoginData] = useState({ method:"email", value:"", otp:"", otpSent:false });
  const [onboardStep, setOnboardStep] = useState(0);
  const [subpage, setSubpage] = useState("dashboard");
  const [selectedScheme, setSelectedScheme] = useState(null);
  const [filterCat, setFilterCat] = useState("All");
  const [filterStatus, setFilterStatus] = useState("All");
  const [chatMsgs, setChatMsgs] = useState([
    { role:"assistant", text:"Hello! I'm your ELIGIFY AI. I've analyzed your profile and I'm ready to help you understand every scheme you're eligible for, explain why you qualify or don't, and guide your application. What would you like to know?" }
  ]);
  const [chatInput, setChatInput] = useState("");
  const [chatLoading, setChatLoading] = useState(false);
  const [familyMembers, setFamilyMembers] = useState([]);
  const [addingMember, setAddingMember] = useState(false);
  const [tempMember, setTempMember] = useState({ name:"", relation:"Father", age:"", gender:"male", income:150000, category:"General", education:"Graduate" });
  const chatEndRef = useRef(null);

  useEffect(() => { chatEndRef.current?.scrollIntoView({ behavior:"smooth" }); }, [chatMsgs]);

  const allEligible = SCHEMES.filter(s => checkEligibility(s, profile).status === "eligible");
  const allPartial  = SCHEMES.filter(s => checkEligibility(s, profile).status === "partial");
  const score = profile.age ? Math.min(96, Math.round((allEligible.length / SCHEMES.length) * 100 * 1.5 + allPartial.length * 3)) : 0;

  // ── LOGIN ──────────────────────────────────────────────────────
  const handleSendOTP = () => {
    if (!loginData.value.trim()) return;
    setLoginData(d => ({ ...d, otpSent:true }));
  };
  const handleVerifyOTP = () => {
    setUser({ id: loginData.value, contact: loginData.value });
    setPage("onboarding");
  };

  // ── CHAT ──────────────────────────────────────────────────────
  const sendChat = async () => {
    if (!chatInput.trim() || chatLoading) return;
    const msg = chatInput.trim(); setChatInput(""); setChatLoading(true);
    setChatMsgs(m => [...m, { role:"user", text:msg }]);

    const schemeDB = SCHEMES.map(s => `"${s.name}": Benefit=${s.benefit}, Eligibility rules: ${s.rules.join("; ")}, Apply at ${s.applyLink}`).join("\n");
    const profileStr = profile.age
      ? `User Profile — Name: ${profile.name||"User"}, Age: ${profile.age}, Gender: ${profile.gender||"not set"}, State: ${profile.state||"not set"}, Category: ${profile.category||"not set"}, Annual family income: ₹${(profile.income||0).toLocaleString()}, Highest education: ${profile.education||"not set"}, Current course: ${profile.course||"not set"}, Institution type: ${profile.institutionType||"not set"}, Class/Year: ${profile.classYear||"not set"}, Academic percentage: ${profile.percentage||"not set"}%, Occupation: ${profile.occupation||"not set"}, Caste certificate available: ${profile.hasCasteCert||"not specified"}, Income certificate available: ${profile.hasIncomeCert||"not specified"}.
Eligible schemes: ${allEligible.map(s=>s.name).join(", ")||"none"}.
Partially eligible: ${allPartial.map(s=>s.name).join(", ")||"none"}.`
      : "User has not completed their profile yet.";

    const systemPrompt = `You are ELIGIFY's AI assistant — a knowledgeable, warm guide helping Indian citizens find and apply for government schemes, scholarships, and welfare programs.

${profileStr}

SCHEME DATABASE (use ONLY these):
${schemeDB}

STRICT RULES:
1. Answer ONLY based on the user's actual profile data and the schemes listed above
2. Be specific — name exact schemes, amounts, deadlines, and rules
3. If profile is incomplete, tell the user exactly what info is missing
4. For eligibility questions, explain rule-by-rule whether each condition is met
5. For application questions, give step-by-step guidance with the official link
6. Never invent schemes not in the database
7. Keep answers focused, helpful, and in plain language (no jargon)
8. Always end with a follow-up suggestion like "Want me to explain the documents needed?" or "Shall I compare your top 3 eligible schemes?"
9. Use ₹ symbol, Indian English style`;

    const GEMINI_KEY = "AQ.Ab8RN6I2dvx8_m0E28SvrQuSiMXqcLYeVP89uFxwIOLK6-cDyg";
    const GEMINI_URL = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${GEMINI_KEY}`;

    // Build full conversation history for context
    const historyParts = chatMsgs.slice(1).map(m => ({
      role: m.role === "assistant" ? "model" : "user",
      parts: [{ text: m.text }]
    }));

    try {
      const res = await fetch(GEMINI_URL, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          system_instruction: { parts: [{ text: systemPrompt }] },
          contents: [
            ...historyParts,
            { role: "user", parts: [{ text: msg }] }
          ],
          generationConfig: {
            temperature: 0.7,
            maxOutputTokens: 1000,
          }
        })
      });
      const data = await res.json();
      const reply = data?.candidates?.[0]?.content?.parts?.[0]?.text || "Sorry, I couldn't get a response. Please try again.";
      setChatMsgs(m => [...m, { role:"assistant", text: reply }]);
    } catch (err) {
      setChatMsgs(m => [...m, { role:"assistant", text:"Network error. Please check your connection and try again." }]);
    }
    setChatLoading(false);
  };

  // ── ONBOARDING STEPS ─────────────────────────────────────────
  const steps = [
    { title:"Personal Details", subtitle:"Tell us about yourself", icon:"👤", color:"#EFF6FF", accent:"#2563EB",
      fields:[
        { key:"name", label:"Full Name", type:"text", placeholder:"e.g. Priya Sharma", required:true },
        { key:"age",  label:"Age", type:"number", placeholder:"e.g. 19" },
        { key:"gender", label:"Gender", type:"select", options:["male","female","other"] },
        { key:"state", label:"State / UT", type:"select", options:["Andhra Pradesh","Arunachal Pradesh","Assam","Bihar","Chhattisgarh","Delhi","Goa","Gujarat","Haryana","Himachal Pradesh","Jharkhand","Karnataka","Kerala","Madhya Pradesh","Maharashtra","Manipur","Meghalaya","Mizoram","Nagaland","Odisha","Punjab","Rajasthan","Sikkim","Tamil Nadu","Telangana","Tripura","Uttar Pradesh","Uttarakhand","West Bengal","Jammu & Kashmir","Ladakh"] },
        { key:"district", label:"District", type:"text", placeholder:"e.g. Gwalior" },
        { key:"religion", label:"Religion", type:"select", options:["Hindu","Muslim","Christian","Sikh","Buddhist","Jain","Other"] },
      ]
    },
    { title:"Education Details", subtitle:"Your academic background", icon:"📚", color:"#F0FDF4", accent:"#16A34A",
      fields:[
        { key:"education", label:"Highest Qualification", type:"select", options:["Below 10th","10th Pass","12th Pass","Diploma","Graduate (pursuing)","Graduate (completed)","Post Graduate","Doctorate"] },
        { key:"course", label:"Course / Stream", type:"text", placeholder:"e.g. B.Tech CSE, 12th Science, MBA" },
        { key:"institutionType", label:"Institution Type", type:"select", options:["Government School","Private School","Government College/University","Private College","IIT/NIT/AIIMS/IIM","Open University","Vocational/ITI","Not currently studying"] },
        { key:"classYear", label:"Class / Year of Study", type:"text", placeholder:"e.g. Class 11, 2nd Year B.Tech" },
        { key:"percentage", label:"Last Academic % / CGPA", type:"number", placeholder:"e.g. 78 (enter percentage)" },
        { key:"board", label:"Exam Board / University", type:"text", placeholder:"e.g. CBSE, MPBSE, VTU" },
      ]
    },
    { title:"Financial & Social", subtitle:"Income and category details", icon:"💼", color:"#FFFBEB", accent:"#D97706",
      fields:[
        { key:"income", label:"Annual Family Income", type:"incomeSelect" },
        { key:"category", label:"Social Category", type:"select", options:["General","OBC","SC","ST","EWS"] },
        { key:"occupation", label:"Your Occupation", type:"select", options:["Student (Full-time)","Student + Part-time work","Employed (Private)","Employed (Govt)","Farmer","Self-employed","Unemployed","Homemaker"] },
        { key:"parentOccupation", label:"Parent/Guardian Occupation", type:"select", options:["Farmer","Daily wage worker","Small business","Salaried (Private)","Salaried (Govt)","Retired","Deceased","Other"] },
        { key:"hasCasteCert", label:"Caste Certificate Available?", type:"select", options:["Yes","No","Not applicable","In process"] },
        { key:"hasIncomeCert", label:"Income Certificate Available?", type:"select", options:["Yes","No","In process"] },
      ]
    },
    { title:"Additional Info", subtitle:"A few more details to unlock more schemes", icon:"📋", color:"#FDF2F8", accent:"#DB2777",
      fields:[
        { key:"domicile", label:"Domicile State", type:"text", placeholder:"Same as state, or specify" },
        { key:"disability", label:"Person with Disability?", type:"select", options:["No","Yes – 40–60%","Yes – 60–80%","Yes – 80%+"] },
        { key:"minority", label:"Minority Community?", type:"select", options:["No","Yes – Muslim","Yes – Christian","Yes – Sikh","Yes – Buddhist","Yes – Parsi","Yes – Jain"] },
        { key:"bankAccount", label:"Bank Account (Aadhaar linked)?", type:"select", options:["Yes – Aadhaar linked","Yes – not linked","No"] },
        { key:"aadhaar", label:"Aadhaar Card Available?", type:"select", options:["Yes","No"] },
        { key:"domicileCert", label:"Domicile Certificate Available?", type:"select", options:["Yes","No","In process"] },
      ]
    },
  ];

  // ─── PAGES ────────────────────────────────────────────────────

  if (page === "landing") return <Landing onLogin={() => setPage("login")} />;

  if (page === "login") return (
    <div style={{ minHeight:"100vh", background:"#F8FAFF", display:"flex", alignItems:"center", justifyContent:"center", fontFamily:"'Inter',sans-serif", padding:"1rem" }}>
      <div style={{ width:"100%", maxWidth:440 }}>
        {/* Logo */}
        <div style={{ textAlign:"center", marginBottom:"2rem" }}>
          <div style={{ display:"inline-flex", alignItems:"center", gap:10, marginBottom:12 }}>
            <div style={{ width:42, height:42, borderRadius:12, background:"linear-gradient(135deg,#2563EB,#3B82F6)", display:"flex", alignItems:"center", justifyContent:"center", fontSize:20 }}>🎯</div>
            <span style={{ fontSize:24, fontWeight:800, color:"#1E293B", letterSpacing:-0.5 }}>ELIGIFY</span>
          </div>
          <div style={{ fontSize:22, fontWeight:700, color:"#1E293B", marginBottom:6 }}>Welcome back</div>
          <div style={{ color:"#64748B", fontSize:14 }}>Log in to discover your eligible schemes</div>
        </div>
        <div style={{ background:"#fff", border:"1px solid #E2E8F0", borderRadius:20, padding:"2rem", boxShadow:"0 4px 24px rgba(0,0,0,0.06)" }}>
          {/* Toggle */}
          <div style={{ display:"flex", background:"#F1F5F9", borderRadius:12, padding:4, marginBottom:"1.5rem" }}>
            {["email","phone"].map(m => (
              <button key={m} onClick={() => setLoginData(d => ({ ...d, method:m, value:"", otpSent:false }))}
                style={{ flex:1, padding:"8px", borderRadius:9, border:"none", background: loginData.method===m ? "#fff":"transparent", color: loginData.method===m ? "#2563EB":"#64748B", fontWeight: loginData.method===m ? 600:400, cursor:"pointer", fontSize:14, boxShadow: loginData.method===m ? "0 1px 4px rgba(0,0,0,0.1)":"none", transition:"all 0.2s" }}>
                {m === "email" ? "📧 Email" : "📱 Phone"}
              </button>
            ))}
          </div>
          {!loginData.otpSent ? (
            <>
              <label style={{ display:"block", fontSize:13, color:"#374151", fontWeight:500, marginBottom:6 }}>
                {loginData.method === "email" ? "Email Address" : "Mobile Number"}
              </label>
              <input type={loginData.method === "email" ? "email" : "tel"}
                value={loginData.value} onChange={e => setLoginData(d => ({ ...d, value:e.target.value }))}
                placeholder={loginData.method === "email" ? "you@example.com" : "+91 98765 43210"}
                style={{ width:"100%", boxSizing:"border-box", padding:"12px 14px", borderRadius:12, border:"1.5px solid #E2E8F0", fontSize:15, color:"#1E293B", outline:"none", marginBottom:"1rem" }} />
              <button onClick={handleSendOTP} disabled={!loginData.value.trim()}
                style={{ width:"100%", padding:"13px", borderRadius:12, border:"none", background: loginData.value.trim() ? "linear-gradient(135deg,#2563EB,#3B82F6)":"#E2E8F0", color: loginData.value.trim() ? "#fff":"#94A3B8", fontWeight:600, fontSize:15, cursor: loginData.value.trim() ? "pointer":"not-allowed" }}>
                Send OTP →
              </button>
            </>
          ) : (
            <>
              <div style={{ background:"#EFF6FF", borderRadius:10, padding:"10px 14px", fontSize:13, color:"#1D4ED8", marginBottom:"1rem" }}>
                OTP sent to <strong>{loginData.value}</strong>
              </div>
              <label style={{ display:"block", fontSize:13, color:"#374151", fontWeight:500, marginBottom:6 }}>Enter OTP</label>
              <input type="text" placeholder="Enter 6-digit OTP" maxLength={6}
                style={{ width:"100%", boxSizing:"border-box", padding:"12px 14px", borderRadius:12, border:"1.5px solid #E2E8F0", fontSize:18, letterSpacing:8, textAlign:"center", color:"#1E293B", outline:"none", marginBottom:"1rem" }} />
              <button onClick={handleVerifyOTP}
                style={{ width:"100%", padding:"13px", borderRadius:12, border:"none", background:"linear-gradient(135deg,#2563EB,#3B82F6)", color:"#fff", fontWeight:600, fontSize:15, cursor:"pointer" }}>
                Verify & Continue ✓
              </button>
              <button onClick={() => setLoginData(d => ({ ...d, otpSent:false }))}
                style={{ width:"100%", marginTop:8, padding:"10px", background:"transparent", border:"none", color:"#64748B", fontSize:13, cursor:"pointer" }}>
                ← Change {loginData.method}
              </button>
            </>
          )}
          <div style={{ textAlign:"center", marginTop:"1.5rem", paddingTop:"1.5rem", borderTop:"1px solid #F1F5F9" }}>
            <span style={{ fontSize:13, color:"#64748B" }}>First time? </span>
            <button onClick={handleVerifyOTP} style={{ background:"none", border:"none", color:"#2563EB", fontSize:13, fontWeight:600, cursor:"pointer" }}>Create free account →</button>
          </div>
        </div>
        <div style={{ textAlign:"center", marginTop:"1.5rem" }}>
          <button onClick={() => { setUser({ id:"guest" }); setPage("onboarding"); }}
            style={{ background:"none", border:"none", color:"#94A3B8", fontSize:13, cursor:"pointer" }}>
            Continue as guest (limited access)
          </button>
        </div>
      </div>
    </div>
  );

  if (page === "onboarding") {
    const step = steps[onboardStep];
    const isLast = onboardStep === steps.length - 1;
    return (
      <div style={{ minHeight:"100vh", background:"#F8FAFF", fontFamily:"'Inter',sans-serif", padding:"2rem 1rem" }}>
        <div style={{ maxWidth:580, margin:"0 auto" }}>
          {/* Header */}
          <div style={{ display:"flex", alignItems:"center", justifyContent:"space-between", marginBottom:"2rem" }}>
            <div style={{ fontSize:20, fontWeight:800, color:"#1E293B" }}>🎯 ELIGIFY</div>
            <div style={{ fontSize:13, color:"#94A3B8" }}>Step {onboardStep+1} of {steps.length}</div>
          </div>
          {/* Progress */}
          <div style={{ display:"flex", gap:6, marginBottom:"2rem" }}>
            {steps.map((_,i) => (
              <div key={i} style={{ flex:1, height:5, borderRadius:99, background: i < onboardStep ? "#2563EB" : i === onboardStep ? "#93C5FD" : "#E2E8F0", transition:"all 0.3s" }} />
            ))}
          </div>
          {/* Card */}
          <div style={{ background:"#fff", borderRadius:24, border:"1px solid #E2E8F0", boxShadow:"0 4px 32px rgba(0,0,0,0.06)", overflow:"hidden" }}>
            <div style={{ background:step.color, padding:"1.5rem 2rem", borderBottom:"1px solid #E2E8F0" }}>
              <div style={{ fontSize:32, marginBottom:6 }}>{step.icon}</div>
              <div style={{ fontSize:20, fontWeight:700, color:"#1E293B" }}>{step.title}</div>
              <div style={{ fontSize:14, color:"#64748B", marginTop:3 }}>{step.subtitle}</div>
            </div>
            <div style={{ padding:"1.75rem 2rem" }}>
              <div style={{ display:"grid", gridTemplateColumns:"1fr 1fr", gap:14 }}>
                {step.fields.map(f => (
                  <div key={f.key} style={{ gridColumn: ["name","course","institutionType","domicile"].includes(f.key) ? "span 2" : "span 1" }}>
                    <label style={{ display:"block", fontSize:12, color:"#475569", fontWeight:600, marginBottom:5, textTransform:"uppercase", letterSpacing:0.5 }}>{f.label}</label>
                    {f.type === "incomeSelect" ? (
                      <select value={profile.income||""} onChange={e => setProfile(p => ({ ...p, income:parseInt(e.target.value) }))}
                        style={selectStyle}>
                        <option value="">Select income range</option>
                        {INCOME_OPTIONS.map(o => <option key={o.value} value={o.value}>{o.label}</option>)}
                      </select>
                    ) : f.type === "select" ? (
                      <select value={profile[f.key]||""} onChange={e => setProfile(p => ({ ...p, [f.key]:e.target.value }))}
                        style={selectStyle}>
                        <option value="">Select...</option>
                        {f.options.map(o => <option key={o} value={o}>{o}</option>)}
                      </select>
                    ) : (
                      <input type={f.type} placeholder={f.placeholder} value={profile[f.key]||""}
                        onChange={e => setProfile(p => ({ ...p, [f.key]:e.target.value }))}
                        style={inputStyle} />
                    )}
                  </div>
                ))}
              </div>
              <div style={{ display:"flex", gap:10, marginTop:"1.75rem" }}>
                {onboardStep > 0 && (
                  <button onClick={() => setOnboardStep(s => s-1)}
                    style={{ flex:1, padding:"12px", borderRadius:12, border:"1.5px solid #E2E8F0", background:"#fff", color:"#475569", cursor:"pointer", fontSize:14, fontWeight:500 }}>
                    ← Back
                  </button>
                )}
                <button onClick={() => isLast ? setPage("main") : setOnboardStep(s => s+1)}
                  style={{ flex:2, padding:"13px", borderRadius:12, border:"none", background:`linear-gradient(135deg,${step.accent},${step.accent}CC)`, color:"#fff", cursor:"pointer", fontSize:15, fontWeight:700 }}>
                  {isLast ? "Analyse My Eligibility ✨" : "Continue →"}
                </button>
              </div>
              <button onClick={() => setPage("main")} style={{ width:"100%", marginTop:10, padding:"8px", background:"transparent", border:"none", color:"#94A3B8", fontSize:12, cursor:"pointer" }}>
                Skip this step
              </button>
            </div>
          </div>
          {/* Trust note */}
          <div style={{ textAlign:"center", marginTop:"1.25rem", fontSize:12, color:"#94A3B8" }}>
            🔒 Your data is used only to match you with eligible schemes. Never shared.
          </div>
        </div>
      </div>
    );
  }

  if (page === "main") {
    const cats = ["All", ...new Set(SCHEMES.map(s => s.category))];
    const displayed = SCHEMES.filter(s => {
      const catOk = filterCat === "All" || s.category === filterCat;
      const el = checkEligibility(s, profile);
      const stOk = filterStatus === "All" || (filterStatus === "Eligible" && el.status === "eligible") || (filterStatus === "Partial" && el.status === "partial") || (filterStatus === "Not Eligible" && el.status === "not_eligible");
      return catOk && stOk;
    });

    const SIDEBAR_ITEMS = [
      { id:"dashboard", icon:"🏠", label:"Dashboard" },
      { id:"opportunities", icon:"🎯", label:"Opportunities", badge: allEligible.length },
      { id:"family", icon:"👨‍👩‍👧", label:"Family Benefits" },
      { id:"radar", icon:"📡", label:"Opportunity Radar" },
      { id:"assistant", icon:"🤖", label:"AI Assistant" },
      { id:"profile", icon:"👤", label:"My Profile" },
    ];

    return (
      <div style={{ display:"flex", minHeight:"100vh", background:"#F8FAFF", fontFamily:"'Inter',sans-serif" }}>
        {/* Sidebar */}
        <div style={{ width:230, background:"#fff", borderRight:"1px solid #E2E8F0", padding:"1.25rem 0.875rem", display:"flex", flexDirection:"column", flexShrink:0 }}>
          <div style={{ display:"flex", alignItems:"center", gap:8, paddingLeft:6, marginBottom:"2rem" }}>
            <div style={{ width:34, height:34, borderRadius:10, background:"linear-gradient(135deg,#2563EB,#3B82F6)", display:"flex", alignItems:"center", justifyContent:"center", fontSize:16 }}>🎯</div>
            <div>
              <div style={{ fontSize:16, fontWeight:800, color:"#1E293B" }}>ELIGIFY</div>
              <div style={{ fontSize:10, color:"#94A3B8", marginTop:-1 }}>AI Eligibility Platform</div>
            </div>
          </div>
          {SIDEBAR_ITEMS.map(item => (
            <button key={item.id} onClick={() => { setSubpage(item.id); setSelectedScheme(null); }}
              style={{ display:"flex", alignItems:"center", gap:10, padding:"10px 12px", borderRadius:10, border:"none", background: subpage===item.id ? "#EFF6FF":"transparent", color: subpage===item.id ? "#2563EB":"#64748B", cursor:"pointer", fontSize:13.5, fontWeight: subpage===item.id ? 600:400, marginBottom:2, width:"100%", textAlign:"left" }}>
              <span style={{ fontSize:16 }}>{item.icon}</span>
              {item.label}
              {item.badge > 0 && <span style={{ marginLeft:"auto", background:"#2563EB", color:"#fff", fontSize:10, fontWeight:700, borderRadius:20, padding:"1px 7px", minWidth:18, textAlign:"center" }}>{item.badge}</span>}
            </button>
          ))}
          <div style={{ marginTop:"auto", paddingTop:"1rem", borderTop:"1px solid #F1F5F9" }}>
            <div style={{ fontSize:12, color:"#94A3B8", paddingLeft:12, marginBottom:6 }}>Logged in as</div>
            <div style={{ fontSize:13, color:"#475569", fontWeight:500, paddingLeft:12, overflow:"hidden", textOverflow:"ellipsis", whiteSpace:"nowrap" }}>{profile.name || user?.id || "Guest"}</div>
            <button onClick={() => setPage("landing")} style={{ display:"flex", alignItems:"center", gap:8, padding:"9px 12px", marginTop:6, width:"100%", background:"transparent", border:"none", color:"#94A3B8", cursor:"pointer", fontSize:12, borderRadius:8 }}>
              ← Exit
            </button>
          </div>
        </div>

        {/* Content */}
        <div style={{ flex:1, overflowY:"auto", maxHeight:"100vh" }}>

          {/* DASHBOARD */}
          {subpage === "dashboard" && (
            <div style={{ padding:"2rem" }}>
              <div style={{ marginBottom:"1.5rem" }}>
                <div style={{ fontSize:24, fontWeight:700, color:"#1E293B" }}>
                  {profile.name ? `Hello, ${profile.name} 👋` : "Your Dashboard"}
                </div>
                <div style={{ color:"#64748B", fontSize:14, marginTop:3 }}>
                  {profile.age ? "Your personalized eligibility analysis is ready." : "Complete your profile to see matched opportunities."}
                </div>
              </div>
              {/* Score banner */}
              <div style={{ background:"linear-gradient(135deg,#EFF6FF,#DBEAFE)", border:"1px solid #BFDBFE", borderRadius:20, padding:"1.5rem 2rem", marginBottom:"1.5rem", display:"flex", alignItems:"center", gap:"2rem", flexWrap:"wrap" }}>
                <div>
                  <div style={{ fontSize:13, color:"#3B82F6", fontWeight:600, marginBottom:4 }}>OPPORTUNITY SCORE</div>
                  <div style={{ fontSize:48, fontWeight:800, color:"#1D4ED8", lineHeight:1 }}>{score}<span style={{ fontSize:22, color:"#60A5FA" }}>/100</span></div>
                  <div style={{ fontSize:13, color:"#3B82F6", marginTop:4 }}>{score >= 70 ? "Excellent profile match!" : score >= 40 ? "Good – a few more fields will help" : "Add profile details to unlock schemes"}</div>
                </div>
                <div style={{ flex:1, minWidth:200 }}>
                  <div style={{ background:"rgba(255,255,255,0.6)", borderRadius:99, height:12, overflow:"hidden", marginBottom:6 }}>
                    <div style={{ width:`${score}%`, height:"100%", background:"linear-gradient(90deg,#2563EB,#60A5FA)", borderRadius:99, transition:"all 1.2s" }} />
                  </div>
                  <div style={{ display:"flex", justifyContent:"space-between", fontSize:11, color:"#60A5FA" }}>
                    <span>Low match</span><span>High match</span>
                  </div>
                </div>
              </div>
              {/* Stats */}
              <div style={{ display:"grid", gridTemplateColumns:"repeat(auto-fit,minmax(150px,1fr))", gap:14, marginBottom:"1.75rem" }}>
                {[
                  { label:"Eligible Now", value:allEligible.length, color:"#16A34A", bg:"#F0FDF4", border:"#BBF7D0", icon:"✅" },
                  { label:"Partially Eligible", value:allPartial.length, color:"#D97706", bg:"#FFFBEB", border:"#FDE68A", icon:"⚡" },
                  { label:"Total Schemes", value:SCHEMES.length, color:"#2563EB", bg:"#EFF6FF", border:"#BFDBFE", icon:"📋" },
                  { label:"Categories", value:[...new Set(allEligible.map(s=>s.category))].length, color:"#DB2777", bg:"#FDF2F8", border:"#FBCFE8", icon:"🗂️" },
                ].map((c,i) => (
                  <div key={i} style={{ background:c.bg, border:`1px solid ${c.border}`, borderRadius:16, padding:"1.25rem" }}>
                    <div style={{ fontSize:24, marginBottom:6 }}>{c.icon}</div>
                    <div style={{ fontSize:28, fontWeight:800, color:c.color }}>{c.value}</div>
                    <div style={{ fontSize:12, color:"#64748B", marginTop:2 }}>{c.label}</div>
                  </div>
                ))}
              </div>
              {/* Eligible list */}
              <div style={{ fontSize:16, fontWeight:700, color:"#1E293B", marginBottom:12 }}>Top Eligible Schemes</div>
              {allEligible.length === 0 ? (
                <div style={{ background:"#fff", border:"1px solid #E2E8F0", borderRadius:16, padding:"2.5rem", textAlign:"center" }}>
                  <div style={{ fontSize:40, marginBottom:10 }}>📝</div>
                  <div style={{ color:"#64748B", fontSize:14, marginBottom:12 }}>Complete your profile to see your eligible schemes</div>
                  <button onClick={() => setSubpage("profile")} style={{ padding:"9px 22px", borderRadius:10, border:"1.5px solid #2563EB", background:"transparent", color:"#2563EB", cursor:"pointer", fontSize:13, fontWeight:600 }}>Update Profile →</button>
                </div>
              ) : (
                allEligible.slice(0,5).map(s => (
                  <DashSchemeRow key={s.id} scheme={s} onClick={() => { setSelectedScheme(s); setSubpage("opportunities"); }} />
                ))
              )}
              {allEligible.length > 5 && (
                <button onClick={() => setSubpage("opportunities")} style={{ width:"100%", padding:"11px", marginTop:6, background:"#EFF6FF", border:"1px solid #BFDBFE", borderRadius:12, color:"#2563EB", cursor:"pointer", fontSize:13, fontWeight:600 }}>
                  View all {allEligible.length} eligible schemes →
                </button>
              )}
            </div>
          )}

          {/* OPPORTUNITIES */}
          {subpage === "opportunities" && (
            <div style={{ padding:"2rem" }}>
              {selectedScheme ? (
                <SchemeDetail scheme={selectedScheme} profile={profile} onBack={() => setSelectedScheme(null)} />
              ) : (
                <>
                  <div style={{ fontSize:22, fontWeight:700, color:"#1E293B", marginBottom:4 }}>Opportunities</div>
                  <div style={{ fontSize:13, color:"#64748B", marginBottom:"1.25rem" }}>{displayed.length} schemes · matched to your profile</div>
                  {/* Filters */}
                  <div style={{ display:"flex", gap:8, marginBottom:"1.25rem", flexWrap:"wrap" }}>
                    {["All","Eligible","Partial","Not Eligible"].map(f => (
                      <button key={f} onClick={() => setFilterStatus(f)}
                        style={{ padding:"6px 14px", borderRadius:20, border:`1.5px solid ${filterStatus===f ? "#2563EB":"#E2E8F0"}`, background: filterStatus===f ? "#EFF6FF":"#fff", color: filterStatus===f ? "#2563EB":"#64748B", cursor:"pointer", fontSize:12, fontWeight: filterStatus===f ? 600:400 }}>
                        {f}
                      </button>
                    ))}
                    <div style={{ width:1, background:"#E2E8F0", margin:"0 4px" }} />
                    {cats.map(c => (
                      <button key={c} onClick={() => setFilterCat(c)}
                        style={{ padding:"6px 14px", borderRadius:20, border:`1.5px solid ${filterCat===c ? "#16A34A":"#E2E8F0"}`, background: filterCat===c ? "#F0FDF4":"#fff", color: filterCat===c ? "#15803D":"#64748B", cursor:"pointer", fontSize:12 }}>
                        {c}
                      </button>
                    ))}
                  </div>
                  <div style={{ display:"grid", gridTemplateColumns:"repeat(auto-fill,minmax(290px,1fr))", gap:14 }}>
                    {displayed.map(s => (
                      <SchemeCard key={s.id} scheme={s} eligibility={checkEligibility(s,profile)} onClick={() => setSelectedScheme(s)} />
                    ))}
                  </div>
                </>
              )}
            </div>
          )}

          {/* FAMILY */}
          {subpage === "family" && (
            <div style={{ padding:"2rem" }}>
              <div style={{ fontSize:22, fontWeight:700, color:"#1E293B", marginBottom:4 }}>Family Benefits</div>
              <div style={{ fontSize:13, color:"#64748B", marginBottom:"1.5rem" }}>Add family members to see the combined benefit potential of your household.</div>
              {familyMembers.map((m,idx) => {
                const mElig = SCHEMES.filter(s => checkEligibility(s,m).status === "eligible");
                return (
                  <div key={idx} style={{ background:"#fff", border:"1px solid #E2E8F0", borderRadius:16, padding:"1.25rem", marginBottom:12 }}>
                    <div style={{ display:"flex", alignItems:"center", gap:12, marginBottom:10 }}>
                      <div style={{ width:42, height:42, borderRadius:"50%", background:"#EFF6FF", display:"flex", alignItems:"center", justifyContent:"center", fontSize:18, color:"#2563EB", fontWeight:700 }}>{m.name[0]?.toUpperCase()}</div>
                      <div style={{ flex:1 }}>
                        <div style={{ fontWeight:700, color:"#1E293B" }}>{m.name} <span style={{ fontWeight:400, color:"#94A3B8", fontSize:12 }}>({m.relation})</span></div>
                        <div style={{ fontSize:12, color:"#64748B" }}>Age {m.age} · {m.gender} · {m.category} · ₹{(m.income||0).toLocaleString()}/yr</div>
                      </div>
                      <span style={{ background: mElig.length > 0 ? "#F0FDF4":"#F8FAFC", border:`1px solid ${mElig.length > 0 ? "#BBF7D0":"#E2E8F0"}`, color: mElig.length > 0 ? "#16A34A":"#94A3B8", fontSize:12, padding:"3px 12px", borderRadius:20, fontWeight:600 }}>{mElig.length} eligible</span>
                    </div>
                    {mElig.length > 0 && (
                      <div style={{ display:"flex", gap:6, flexWrap:"wrap" }}>
                        {mElig.slice(0,3).map(s => (
                          <span key={s.id} style={{ fontSize:11, background:"#F1F5F9", border:"1px solid #E2E8F0", borderRadius:20, padding:"3px 10px", color:"#475569" }}>{s.name}</span>
                        ))}
                        {mElig.length > 3 && <span style={{ fontSize:11, color:"#94A3B8" }}>+{mElig.length-3} more</span>}
                      </div>
                    )}
                  </div>
                );
              })}
              {addingMember ? (
                <div style={{ background:"#fff", border:"1.5px solid #BFDBFE", borderRadius:18, padding:"1.5rem" }}>
                  <div style={{ fontWeight:700, color:"#1E293B", marginBottom:14 }}>Add Family Member</div>
                  <div style={{ display:"grid", gridTemplateColumns:"1fr 1fr", gap:12 }}>
                    {[
                      { key:"name", label:"Name", type:"text", placeholder:"e.g. Ramesh" },
                      { key:"relation", label:"Relation", type:"select", options:["Father","Mother","Sibling","Child","Grandparent","Spouse"] },
                      { key:"age", label:"Age", type:"number", placeholder:"e.g. 45" },
                      { key:"gender", label:"Gender", type:"select", options:["male","female","other"] },
                      { key:"education", label:"Education", type:"select", options:["Below 10th","10th Pass","12th Pass","Graduate","Post Graduate"] },
                      { key:"category", label:"Category", type:"select", options:["General","OBC","SC","ST","EWS"] },
                    ].map(f => (
                      <div key={f.key}>
                        <label style={{ display:"block", fontSize:11, color:"#475569", fontWeight:600, marginBottom:4, textTransform:"uppercase", letterSpacing:0.5 }}>{f.label}</label>
                        {f.type === "select" ? (
                          <select value={tempMember[f.key]||""} onChange={e => setTempMember(m => ({ ...m, [f.key]:e.target.value }))} style={selectStyle}>
                            {f.options.map(o => <option key={o} value={o}>{o}</option>)}
                          </select>
                        ) : (
                          <input type={f.type} placeholder={f.placeholder} value={tempMember[f.key]||""}
                            onChange={e => setTempMember(m => ({ ...m, [f.key]:e.target.value }))} style={inputStyle} />
                        )}
                      </div>
                    ))}
                    <div>
                      <label style={{ display:"block", fontSize:11, color:"#475569", fontWeight:600, marginBottom:4, textTransform:"uppercase", letterSpacing:0.5 }}>Annual Income</label>
                      <select value={tempMember.income} onChange={e => setTempMember(m => ({ ...m, income:parseInt(e.target.value) }))} style={selectStyle}>
                        {INCOME_OPTIONS.map(o => <option key={o.value} value={o.value}>{o.label}</option>)}
                      </select>
                    </div>
                  </div>
                  <div style={{ display:"flex", gap:10, marginTop:16 }}>
                    <button onClick={() => setAddingMember(false)} style={{ flex:1, padding:"11px", borderRadius:10, border:"1.5px solid #E2E8F0", background:"#fff", color:"#64748B", cursor:"pointer", fontSize:13 }}>Cancel</button>
                    <button onClick={() => { if (tempMember.name) { setFamilyMembers(m => [...m, { ...tempMember }]); setAddingMember(false); setTempMember({ name:"", relation:"Father", age:"", gender:"male", income:150000, category:"General", education:"Graduate" }); } }}
                      style={{ flex:2, padding:"11px", borderRadius:10, border:"none", background:"linear-gradient(135deg,#2563EB,#3B82F6)", color:"#fff", cursor:"pointer", fontWeight:600, fontSize:13 }}>
                      Add Member ✓
                    </button>
                  </div>
                </div>
              ) : (
                <button onClick={() => setAddingMember(true)} style={{ width:"100%", padding:"16px", borderRadius:16, border:"2px dashed #BFDBFE", background:"#F8FAFF", color:"#2563EB", cursor:"pointer", fontSize:14, fontWeight:600 }}>
                  + Add Family Member
                </button>
              )}
            </div>
          )}

          {/* RADAR */}
          {subpage === "radar" && (
            <div style={{ padding:"2rem" }}>
              <div style={{ fontSize:22, fontWeight:700, color:"#1E293B", marginBottom:4 }}>Opportunity Radar</div>
              <div style={{ fontSize:13, color:"#64748B", marginBottom:"1.75rem" }}>Track deadlines and never miss a scheme.</div>
              {[
                { label:"Open & Active", color:"#16A34A", bg:"#F0FDF4", border:"#BBF7D0", dot:"#22C55E", filter:(s) => s.deadline !== "Ongoing" && new Date(s.deadline) > new Date() },
                { label:"Ongoing (No Deadline)", color:"#2563EB", bg:"#EFF6FF", border:"#BFDBFE", dot:"#3B82F6", filter:(s) => s.deadline === "Ongoing" },
                { label:"Deadline Passed", color:"#DC2626", bg:"#FEF2F2", border:"#FECACA", dot:"#EF4444", filter:(s) => s.deadline !== "Ongoing" && new Date(s.deadline) < new Date() },
              ].map(({ label, color, bg, border, dot, filter }) => {
                const group = SCHEMES.filter(filter);
                return (
                  <div key={label} style={{ marginBottom:"1.75rem" }}>
                    <div style={{ display:"flex", alignItems:"center", gap:8, marginBottom:10 }}>
                      <div style={{ width:8, height:8, borderRadius:"50%", background:dot }} />
                      <div style={{ fontWeight:700, color, fontSize:14 }}>{label}</div>
                      <span style={{ fontSize:12, color:"#94A3B8" }}>({group.length})</span>
                    </div>
                    {group.length === 0 && <div style={{ fontSize:13, color:"#CBD5E1", paddingLeft:16 }}>None</div>}
                    {group.map(s => {
                      const el = checkEligibility(s, profile);
                      return (
                        <div key={s.id} onClick={() => { setSelectedScheme(s); setSubpage("opportunities"); }}
                          style={{ background:"#fff", border:`1px solid ${el.status==="eligible" ? "#BBF7D0":"#E2E8F0"}`, borderRadius:14, padding:"1rem 1.25rem", marginBottom:8, cursor:"pointer", display:"flex", alignItems:"center", gap:14 }}>
                          <span style={{ fontSize:22 }}>{s.icon}</span>
                          <div style={{ flex:1, minWidth:0 }}>
                            <div style={{ fontWeight:600, color:"#1E293B", fontSize:14, overflow:"hidden", textOverflow:"ellipsis", whiteSpace:"nowrap" }}>{s.name}</div>
                            <div style={{ fontSize:12, color:"#64748B", marginTop:2 }}>{s.deadline === "Ongoing" ? "Always open" : `Deadline: ${s.deadline}`} · {s.benefit}</div>
                          </div>
                          {el.status === "eligible" && <span style={{ background:"#F0FDF4", border:"1px solid #BBF7D0", color:"#16A34A", fontSize:11, padding:"3px 10px", borderRadius:20, fontWeight:600, flexShrink:0 }}>Eligible ✓</span>}
                        </div>
                      );
                    })}
                  </div>
                );
              })}
            </div>
          )}

          {/* AI ASSISTANT */}
          {subpage === "assistant" && (
            <div style={{ padding:"2rem", display:"flex", flexDirection:"column", height:"calc(100vh - 4rem)" }}>
              <div style={{ marginBottom:"1.25rem" }}>
                <div style={{ fontSize:22, fontWeight:700, color:"#1E293B", marginBottom:2 }}>AI Assistant</div>
                <div style={{ fontSize:13, color:"#64748B" }}>Ask anything about your eligibility, documents, or how to apply. I know your full profile.</div>
              </div>
              {/* Profile context bar */}
              {profile.age && (
                <div style={{ background:"#F0FDF4", border:"1px solid #BBF7D0", borderRadius:12, padding:"10px 14px", marginBottom:"1rem", fontSize:12, color:"#16A34A", display:"flex", alignItems:"center", gap:8 }}>
                  <span>🔗</span>
                  <span>Connected to your profile · Age {profile.age}, {profile.category||"—"}, ₹{(profile.income||0).toLocaleString()}/yr · {allEligible.length} eligible schemes</span>
                </div>
              )}
              {/* Messages */}
              <div style={{ flex:1, overflowY:"auto", display:"flex", flexDirection:"column", gap:14, paddingBottom:"0.5rem" }}>
                {chatMsgs.map((msg,i) => (
                  <div key={i} style={{ display:"flex", gap:10, justifyContent: msg.role==="user" ? "flex-end":"flex-start", alignItems:"flex-start" }}>
                    {msg.role === "assistant" && (
                      <div style={{ width:34, height:34, borderRadius:"50%", background:"linear-gradient(135deg,#2563EB,#3B82F6)", display:"flex", alignItems:"center", justifyContent:"center", fontSize:16, flexShrink:0, marginTop:2 }}>🤖</div>
                    )}
                    <div style={{ maxWidth:"72%", background: msg.role==="user" ? "linear-gradient(135deg,#2563EB,#3B82F6)":"#fff", border: msg.role==="user" ? "none":"1px solid #E2E8F0", borderRadius: msg.role==="user" ? "18px 18px 4px 18px":"18px 18px 18px 4px", padding:"12px 16px", fontSize:14, lineHeight:1.65, color: msg.role==="user" ? "#fff":"#1E293B", whiteSpace:"pre-wrap", boxShadow: msg.role==="assistant" ? "0 2px 8px rgba(0,0,0,0.04)":"none" }}>
                      {msg.text}
                    </div>
                  </div>
                ))}
                {chatLoading && (
                  <div style={{ display:"flex", gap:10, alignItems:"flex-start" }}>
                    <div style={{ width:34, height:34, borderRadius:"50%", background:"linear-gradient(135deg,#2563EB,#3B82F6)", display:"flex", alignItems:"center", justifyContent:"center", fontSize:16 }}>🤖</div>
                    <div style={{ background:"#fff", border:"1px solid #E2E8F0", borderRadius:"18px 18px 18px 4px", padding:"14px 18px", display:"flex", gap:5, alignItems:"center" }}>
                      {[0,1,2].map(d => <div key={d} style={{ width:7, height:7, borderRadius:"50%", background:"#93C5FD", animation:`bounce 1.2s ${d*0.15}s infinite` }} />)}
                    </div>
                  </div>
                )}
                <div ref={chatEndRef} />
              </div>
              {/* Quick prompts */}
              <div style={{ display:"flex", gap:6, marginBottom:10, flexWrap:"wrap" }}>
                {["Which scheme should I apply first?","What documents do I need?","Why am I not eligible for NSP?","Explain PM-JAY health scheme","How to apply for NSP scholarship?"].map(q => (
                  <button key={q} onClick={() => setChatInput(q)} style={{ fontSize:11, padding:"5px 12px", borderRadius:20, border:"1.5px solid #BFDBFE", background:"#EFF6FF", color:"#2563EB", cursor:"pointer", fontWeight:500 }}>{q}</button>
                ))}
              </div>
              {/* Input */}
              <div style={{ display:"flex", gap:10, background:"#fff", border:"1.5px solid #E2E8F0", borderRadius:16, padding:"8px 8px 8px 16px", boxShadow:"0 2px 12px rgba(0,0,0,0.06)" }}>
                <input value={chatInput} onChange={e => setChatInput(e.target.value)} onKeyDown={e => e.key==="Enter" && sendChat()}
                  placeholder="Ask about any scheme, your eligibility, or required documents..."
                  style={{ flex:1, border:"none", outline:"none", fontSize:14, color:"#1E293B", background:"transparent" }} />
                <button onClick={sendChat} disabled={chatLoading || !chatInput.trim()}
                  style={{ padding:"10px 18px", borderRadius:12, border:"none", background: chatInput.trim() ? "linear-gradient(135deg,#2563EB,#3B82F6)":"#F1F5F9", color: chatInput.trim() ? "#fff":"#94A3B8", cursor: chatInput.trim() ? "pointer":"not-allowed", fontSize:14, fontWeight:600, transition:"all 0.2s" }}>
                  Send →
                </button>
              </div>
            </div>
          )}

          {/* PROFILE */}
          {subpage === "profile" && (
            <div style={{ padding:"2rem", maxWidth:660 }}>
              <div style={{ fontSize:22, fontWeight:700, color:"#1E293B", marginBottom:"1.5rem" }}>My Profile</div>
              {steps.map((step, si) => (
                <div key={si} style={{ background:"#fff", border:"1px solid #E2E8F0", borderRadius:18, overflow:"hidden", marginBottom:"1.25rem" }}>
                  <div style={{ background:step.color, padding:"1rem 1.5rem", display:"flex", alignItems:"center", gap:10 }}>
                    <span style={{ fontSize:20 }}>{step.icon}</span>
                    <div style={{ fontWeight:700, color:"#1E293B" }}>{step.title}</div>
                  </div>
                  <div style={{ padding:"1.25rem 1.5rem", display:"grid", gridTemplateColumns:"1fr 1fr", gap:12 }}>
                    {step.fields.map(f => (
                      <div key={f.key} style={{ gridColumn:["name","course","institutionType","domicile"].includes(f.key) ? "span 2":"span 1" }}>
                        <label style={{ display:"block", fontSize:11, color:"#475569", fontWeight:600, marginBottom:4, textTransform:"uppercase", letterSpacing:0.5 }}>{f.label}</label>
                        {f.type === "incomeSelect" ? (
                          <select value={profile.income||""} onChange={e => setProfile(p => ({ ...p, income:parseInt(e.target.value) }))} style={selectStyle}>
                            <option value="">Select...</option>
                            {INCOME_OPTIONS.map(o => <option key={o.value} value={o.value}>{o.label}</option>)}
                          </select>
                        ) : f.type === "select" ? (
                          <select value={profile[f.key]||""} onChange={e => setProfile(p => ({ ...p, [f.key]:e.target.value }))} style={selectStyle}>
                            <option value="">Select...</option>
                            {f.options.map(o => <option key={o} value={o}>{o}</option>)}
                          </select>
                        ) : (
                          <input type={f.type} value={profile[f.key]||""}
                            onChange={e => setProfile(p => ({ ...p, [f.key]:e.target.value }))}
                            placeholder={f.placeholder} style={inputStyle} />
                        )}
                      </div>
                    ))}
                  </div>
                </div>
              ))}
              <div style={{ background:"#F0FDF4", border:"1px solid #BBF7D0", borderRadius:12, padding:"1rem", fontSize:13, color:"#16A34A" }}>
                ✅ Profile auto-saves. Your eligibility score updates instantly as you make changes.
              </div>
            </div>
          )}
        </div>
      </div>
    );
  }
  return null;
}

// ── SUB-COMPONENTS ─────────────────────────────────────────────────
function DashSchemeRow({ scheme, onClick }) {
  const cat = CATEGORY_COLORS[scheme.category] || CATEGORY_COLORS.Scholarship;
  return (
    <div onClick={onClick} style={{ background:"#fff", border:`1px solid ${cat.border}`, borderRadius:14, padding:"1rem 1.25rem", marginBottom:10, cursor:"pointer", display:"flex", alignItems:"center", gap:14, transition:"box-shadow 0.2s" }}>
      <div style={{ width:40, height:40, borderRadius:12, background:cat.light, display:"flex", alignItems:"center", justifyContent:"center", fontSize:20, flexShrink:0 }}>{scheme.icon}</div>
      <div style={{ flex:1, minWidth:0 }}>
        <div style={{ fontWeight:600, color:"#1E293B", fontSize:14, overflow:"hidden", textOverflow:"ellipsis", whiteSpace:"nowrap" }}>{scheme.name}</div>
        <div style={{ fontSize:12, color:"#64748B", marginTop:2 }}>{scheme.ministry} · {scheme.benefit}</div>
      </div>
      <div style={{ display:"flex", flexDirection:"column", alignItems:"flex-end", gap:4, flexShrink:0 }}>
        <span style={{ background:"#F0FDF4", border:"1px solid #BBF7D0", color:"#16A34A", fontSize:11, padding:"3px 10px", borderRadius:20, fontWeight:600 }}>✓ Eligible</span>
        <span style={{ fontSize:11, color:"#94A3B8" }}>→</span>
      </div>
    </div>
  );
}

function SchemeCard({ scheme, eligibility, onClick }) {
  const cat = CATEGORY_COLORS[scheme.category] || CATEGORY_COLORS.Scholarship;
  const statusMap = {
    eligible: { label:"✓ Eligible", bg:"#F0FDF4", border:"#BBF7D0", color:"#16A34A" },
    partial:  { label:"⚡ Partial", bg:"#FFFBEB", border:"#FDE68A", color:"#D97706" },
    not_eligible: { label:"✗ Not Eligible", bg:"#FEF2F2", border:"#FECACA", color:"#DC2626" },
    unknown:  { label:"? Check Profile", bg:"#F8FAFC", border:"#E2E8F0", color:"#94A3B8" },
  };
  const st = statusMap[eligibility.status] || statusMap.unknown;
  return (
    <div onClick={onClick} style={{ background:"#fff", border:`1px solid ${eligibility.status==="eligible" ? "#BBF7D0":"#E2E8F0"}`, borderRadius:18, overflow:"hidden", cursor:"pointer", transition:"box-shadow 0.2s", position:"relative" }}>
      {eligibility.status === "eligible" && <div style={{ height:3, background:"linear-gradient(90deg,#16A34A,#4ADE80)" }} />}
      <div style={{ padding:"1.25rem" }}>
        <div style={{ display:"flex", alignItems:"flex-start", justifyContent:"space-between", marginBottom:10, gap:8 }}>
          <div style={{ display:"flex", alignItems:"center", gap:8 }}>
            <span style={{ fontSize:22 }}>{scheme.icon}</span>
            <span style={{ fontSize:11, fontWeight:600, background:cat.light, color:cat.tag, border:`1px solid ${cat.border}`, borderRadius:20, padding:"2px 10px" }}>{scheme.category}</span>
          </div>
          <span style={{ fontSize:11, fontWeight:600, background:st.bg, color:st.color, border:`1px solid ${st.border}`, borderRadius:20, padding:"3px 10px", flexShrink:0 }}>{st.label}</span>
        </div>
        <div style={{ fontWeight:700, color:"#1E293B", fontSize:14, marginBottom:5, lineHeight:1.4 }}>{scheme.name}</div>
        <div style={{ fontSize:12, color:"#64748B", marginBottom:10 }}>{scheme.ministry}</div>
        <div style={{ display:"flex", alignItems:"center", justifyContent:"space-between" }}>
          <div style={{ fontSize:14, fontWeight:700, color:cat.accent }}>{scheme.benefit}</div>
          <div style={{ fontSize:11, color:"#94A3B8" }}>{scheme.deadline === "Ongoing" ? "Ongoing" : scheme.deadline}</div>
        </div>
      </div>
    </div>
  );
}

function SchemeDetail({ scheme, profile, onBack }) {
  const el = checkEligibility(scheme, profile);
  const isEligible = el.status === "eligible";
  const cat = CATEGORY_COLORS[scheme.category] || CATEGORY_COLORS.Scholarship;
  return (
    <div style={{ maxWidth:700 }}>
      <button onClick={onBack} style={{ display:"flex", alignItems:"center", gap:6, background:"transparent", border:"none", color:"#64748B", cursor:"pointer", fontSize:13, marginBottom:"1.25rem", padding:0, fontWeight:500 }}>
        ← Back to Opportunities
      </button>
      {isEligible && (
        <div style={{ background:"#F0FDF4", border:"1px solid #BBF7D0", borderRadius:12, padding:"10px 16px", marginBottom:"1rem", fontSize:13, color:"#16A34A", fontWeight:600, display:"flex", alignItems:"center", gap:8 }}>
          ✅ You are eligible for this scheme based on your profile!
        </div>
      )}
      <div style={{ background:"#fff", border:"1px solid #E2E8F0", borderRadius:22, overflow:"hidden", boxShadow:"0 4px 24px rgba(0,0,0,0.06)" }}>
        <div style={{ background:cat.light, padding:"1.75rem 2rem", borderBottom:"1px solid #E2E8F0" }}>
          <div style={{ display:"flex", gap:8, marginBottom:12, flexWrap:"wrap" }}>
            <span style={{ fontSize:11, padding:"3px 12px", borderRadius:20, background:"#fff", border:`1px solid ${cat.border}`, color:cat.tag, fontWeight:600 }}>{scheme.category}</span>
            <span style={{ fontSize:11, padding:"3px 12px", borderRadius:20, background:"#fff", border:"1px solid #E2E8F0", color:"#64748B" }}>{scheme.tag}</span>
            <span style={{ fontSize:11, padding:"3px 12px", borderRadius:20, background:"#fff", border:"1px solid #E2E8F0", color:"#64748B" }}>{scheme.source}</span>
          </div>
          <div style={{ display:"flex", alignItems:"center", gap:12, marginBottom:8 }}>
            <span style={{ fontSize:36 }}>{scheme.icon}</span>
            <div style={{ fontSize:22, fontWeight:800, color:"#1E293B", lineHeight:1.2 }}>{scheme.name}</div>
          </div>
          <div style={{ fontSize:14, color:"#475569" }}>{scheme.ministry}</div>
        </div>
        <div style={{ padding:"1.75rem 2rem" }}>
          <div style={{ fontSize:15, color:"#374151", lineHeight:1.7, marginBottom:"1.5rem" }}>{scheme.description}</div>
          {/* Key Info */}
          <div style={{ display:"grid", gridTemplateColumns:"1fr 1fr", gap:12, marginBottom:"1.5rem" }}>
            {[
              { label:"Benefit Amount", value:scheme.benefit, icon:"💰" },
              { label:"Deadline", value:scheme.deadline, icon:"📅" },
              { label:"State Coverage", value:scheme.state, icon:"📍" },
              { label:"Eligible Categories", value:scheme.categories.join(", "), icon:"👥" },
            ].map(item => (
              <div key={item.label} style={{ background:"#F8FAFC", borderRadius:12, padding:"0.875rem 1rem" }}>
                <div style={{ fontSize:11, color:"#64748B", marginBottom:4, fontWeight:500 }}>{item.icon} {item.label}</div>
                <div style={{ fontSize:14, fontWeight:600, color:"#1E293B" }}>{item.value}</div>
              </div>
            ))}
          </div>
          {/* Eligibility rules */}
          <div style={{ marginBottom:"1.5rem" }}>
            <div style={{ fontWeight:700, color:"#1E293B", marginBottom:10, fontSize:15 }}>Eligibility Rules</div>
            {scheme.rules.map((r, i) => (
              <div key={i} style={{ display:"flex", alignItems:"center", gap:10, padding:"8px 12px", borderRadius:10, background:"#F8FAFC", border:"1px solid #E2E8F0", marginBottom:6 }}>
                <span style={{ fontSize:14 }}>📌</span>
                <span style={{ fontSize:13, color:"#374151" }}>{r}</span>
              </div>
            ))}
          </div>
          {/* Profile check */}
          {el.reasons.length > 0 && (
            <div style={{ marginBottom:"1.5rem" }}>
              <div style={{ fontWeight:700, color:"#1E293B", marginBottom:10, fontSize:15 }}>Your Eligibility Check</div>
              {el.reasons.map((r,i) => (
                <div key={i} style={{ display:"flex", alignItems:"flex-start", gap:10, padding:"10px 14px", borderRadius:12, background: r.pass ? "#F0FDF4":"#FEF2F2", border:`1px solid ${r.pass ? "#BBF7D0":"#FECACA"}`, marginBottom:7 }}>
                  <span style={{ fontSize:16, flexShrink:0 }}>{r.pass ? "✅":"❌"}</span>
                  <span style={{ fontSize:13, color: r.pass ? "#15803D":"#DC2626", lineHeight:1.5 }}>{r.text}</span>
                </div>
              ))}
            </div>
          )}
          {/* Documents */}
          <div style={{ marginBottom:"1.5rem" }}>
            <div style={{ fontWeight:700, color:"#1E293B", marginBottom:10, fontSize:15 }}>Documents Required</div>
            <div style={{ display:"flex", flexWrap:"wrap", gap:8 }}>
              {scheme.documents.map(d => (
                <span key={d} style={{ fontSize:12, background:"#EFF6FF", border:"1px solid #BFDBFE", borderRadius:20, padding:"4px 12px", color:"#1D4ED8", fontWeight:500 }}>📄 {d}</span>
              ))}
            </div>
          </div>
          {/* Apply */}
          <a href={scheme.applyLink} target="_blank" rel="noreferrer"
            style={{ display:"flex", alignItems:"center", justifyContent:"center", gap:8, width:"100%", boxSizing:"border-box", padding:"15px", borderRadius:14, border:"none", background: isEligible ? "linear-gradient(135deg,#059669,#16A34A)":"linear-gradient(135deg,#2563EB,#3B82F6)", color:"#fff", cursor:"pointer", fontSize:16, fontWeight:700, textDecoration:"none" }}>
            Apply Now — Official Portal 🔗
          </a>
          <div style={{ textAlign:"center", marginTop:8, fontSize:11, color:"#94A3B8" }}>Opens: {scheme.applyLink}</div>
        </div>
      </div>
    </div>
  );
}

function Landing({ onLogin }) {
  const features = [
    { icon:"🎯", title:"One Profile", desc:"Enter your details once — age, income, category, education. Done." },
    { icon:"🤖", title:"AI Analysis", desc:"Our AI matches your profile against every rule of every scheme instantly." },
    { icon:"✅", title:"Clear Results", desc:"See exactly which schemes you qualify for, and precisely why." },
    { icon:"🔗", title:"Direct Apply", desc:"One click to the official government portal. No middlemen, ever." },
  ];
  const stats = [{ n:"14+", l:"Verified Schemes" }, { n:"₹5L+", l:"Max Annual Benefit" }, { n:"100%", l:"Free Forever" }, { n:"AI", l:"Powered Match" }];
  const cats = [
    { icon:"🎓", label:"Scholarships", color:"#EFF6FF", accent:"#2563EB", count:"8 schemes" },
    { icon:"🏥", label:"Healthcare", color:"#F0FDF4", accent:"#16A34A", count:"1 scheme" },
    { icon:"🏠", label:"Housing", color:"#FFFBEB", accent:"#D97706", count:"1 scheme" },
    { icon:"🌾", label:"Farmer", color:"#F0FDF4", accent:"#15803D", count:"1 scheme" },
    { icon:"👧", label:"Girl Child", color:"#FDF2F8", accent:"#DB2777", count:"2 schemes" },
  ];
  return (
    <div style={{ minHeight:"100vh", background:"#fff", fontFamily:"'Inter',sans-serif", color:"#1E293B", overflowX:"hidden" }}>
      {/* Nav */}
      <nav style={{ display:"flex", alignItems:"center", justifyContent:"space-between", padding:"1.25rem 3rem", borderBottom:"1px solid #F1F5F9", position:"sticky", top:0, background:"rgba(255,255,255,0.95)", backdropFilter:"blur(12px)", zIndex:50 }}>
        <div style={{ display:"flex", alignItems:"center", gap:10 }}>
          <div style={{ width:36, height:36, borderRadius:10, background:"linear-gradient(135deg,#2563EB,#3B82F6)", display:"flex", alignItems:"center", justifyContent:"center", fontSize:18 }}>🎯</div>
          <span style={{ fontSize:20, fontWeight:800, color:"#1E293B", letterSpacing:-0.5 }}>ELIGIFY</span>
        </div>
        <div style={{ display:"flex", gap:10 }}>
          <button onClick={onLogin} style={{ padding:"9px 20px", borderRadius:10, border:"1.5px solid #E2E8F0", background:"#fff", color:"#475569", cursor:"pointer", fontSize:13, fontWeight:500 }}>Login</button>
          <button onClick={onLogin} style={{ padding:"9px 20px", borderRadius:10, border:"none", background:"linear-gradient(135deg,#2563EB,#3B82F6)", color:"#fff", cursor:"pointer", fontSize:13, fontWeight:600 }}>Get Started Free →</button>
        </div>
      </nav>

      {/* HERO */}
      <div style={{ display:"grid", gridTemplateColumns:"1fr 1fr", gap:"4rem", maxWidth:1100, margin:"0 auto", padding:"5rem 3rem 4rem", alignItems:"center" }}>
        <div>
          <div style={{ display:"inline-flex", alignItems:"center", gap:8, background:"#EFF6FF", border:"1px solid #BFDBFE", borderRadius:20, padding:"5px 14px", fontSize:12, color:"#2563EB", fontWeight:600, marginBottom:"1.5rem" }}>
            🤖 AI-Powered Eligibility Intelligence
          </div>
          <h1 style={{ fontSize:"clamp(2rem,4vw,3.5rem)", fontWeight:800, lineHeight:1.1, margin:"0 0 1.25rem", letterSpacing:-1.5, color:"#0F172A" }}>
            Stop Missing<br />
            <span style={{ background:"linear-gradient(135deg,#2563EB,#7C3AED)", WebkitBackgroundClip:"text", WebkitTextFillColor:"transparent" }}>Government Benefits</span><br />
            You Deserve
          </h1>
          <p style={{ fontSize:17, color:"#64748B", lineHeight:1.7, marginBottom:"2rem", maxWidth:480 }}>
            ELIGIFY analyses your profile and instantly tells you every scholarship, scheme, and welfare program you qualify for — with clear explanations and direct application links.
          </p>
          <div style={{ display:"flex", gap:12, flexWrap:"wrap" }}>
            <button onClick={onLogin} style={{ padding:"14px 30px", borderRadius:12, border:"none", background:"linear-gradient(135deg,#2563EB,#3B82F6)", color:"#fff", cursor:"pointer", fontSize:15, fontWeight:700, boxShadow:"0 8px 24px rgba(37,99,235,0.3)" }}>
              Check My Eligibility →
            </button>
            <button onClick={onLogin} style={{ padding:"14px 26px", borderRadius:12, border:"1.5px solid #E2E8F0", background:"#F8FAFF", color:"#475569", cursor:"pointer", fontSize:15, fontWeight:500 }}>
              Try Demo
            </button>
          </div>
          {/* Trust tags */}
          <div style={{ display:"flex", gap:8, marginTop:"1.5rem", flexWrap:"wrap" }}>
            {["✅ 100% Free","🔒 Data Private","🏛️ Govt Verified Schemes","⚡ Instant Analysis"].map(t => (
              <span key={t} style={{ fontSize:12, color:"#64748B", background:"#F8FAFC", border:"1px solid #E2E8F0", borderRadius:20, padding:"4px 12px" }}>{t}</span>
            ))}
          </div>
        </div>
        {/* Student Image via SVG illustration */}
        <div style={{ position:"relative" }}>
          <div style={{ background:"linear-gradient(135deg,#EFF6FF,#F0FDF4)", borderRadius:28, padding:"2rem", boxShadow:"0 20px 60px rgba(37,99,235,0.12)" }}>
            <svg viewBox="0 0 380 340" xmlns="http://www.w3.org/2000/svg" style={{ width:"100%", height:"auto" }}>
              {/* Desk */}
              <rect x="30" y="260" width="320" height="14" rx="4" fill="#CBD5E1"/>
              <rect x="60" y="274" width="18" height="50" rx="3" fill="#94A3B8"/>
              <rect x="302" y="274" width="18" height="50" rx="3" fill="#94A3B8"/>
              {/* Laptop */}
              <rect x="100" y="185" width="180" height="115" rx="10" fill="#1E293B"/>
              <rect x="107" y="192" width="166" height="100" rx="6" fill="#0EA5E9"/>
              {/* Screen content */}
              <rect x="115" y="200" width="75" height="8" rx="3" fill="rgba(255,255,255,0.7)"/>
              <rect x="115" y="213" width="55" height="5" rx="2" fill="rgba(255,255,255,0.4)"/>
              <rect x="115" y="222" width="65" height="5" rx="2" fill="rgba(255,255,255,0.4)"/>
              <rect x="115" y="231" width="45" height="5" rx="2" fill="rgba(255,255,255,0.4)"/>
              {/* Charts on screen */}
              <rect x="198" y="200" width="68" height="85" rx="4" fill="rgba(255,255,255,0.1)"/>
              <rect x="204" y="245" width="10" height="34" rx="2" fill="#4ADE80"/>
              <rect x="218" y="235" width="10" height="44" rx="2" fill="#60A5FA"/>
              <rect x="232" y="225" width="10" height="54" rx="2" fill="#A78BFA"/>
              <rect x="246" y="240" width="10" height="39" rx="2" fill="#F59E0B"/>
              {/* Laptop base */}
              <rect x="80" y="298" width="220" height="8" rx="4" fill="#334155"/>
              {/* Student */}
              {/* Body */}
              <ellipse cx="190" cy="170" rx="28" ry="36" fill="#DBEAFE"/>
              <rect x="162" y="185" width="56" height="40" rx="10" fill="#2563EB"/>
              {/* Head */}
              <circle cx="190" cy="130" r="30" fill="#FDE68A"/>
              {/* Hair */}
              <ellipse cx="190" cy="105" rx="30" ry="12" fill="#1E293B"/>
              <rect x="160" y="105" width="60" height="10" fill="#1E293B"/>
              {/* Face */}
              <circle cx="180" cy="128" r="3" fill="#92400E"/>
              <circle cx="200" cy="128" r="3" fill="#92400E"/>
              <path d="M183 140 Q190 147 197 140" stroke="#92400E" strokeWidth="2" fill="none" strokeLinecap="round"/>
              {/* Glasses */}
              <rect x="173" y="122" width="14" height="10" rx="3" fill="none" stroke="#1E293B" strokeWidth="1.5"/>
              <rect x="193" y="122" width="14" height="10" rx="3" fill="none" stroke="#1E293B" strokeWidth="1.5"/>
              <line x1="187" y1="127" x2="193" y2="127" stroke="#1E293B" strokeWidth="1.5"/>
              {/* Arms */}
              <path d="M162 195 Q135 210 140 240" stroke="#FDE68A" strokeWidth="12" fill="none" strokeLinecap="round"/>
              <path d="M218 195 Q245 210 240 240" stroke="#FDE68A" strokeWidth="12" fill="none" strokeLinecap="round"/>
              {/* Floating badges */}
              <rect x="10" y="60" width="90" height="36" rx="10" fill="#fff" stroke="#BFDBFE" strokeWidth="1.5"/>
              <text x="20" y="76" fontSize="9" fill="#2563EB" fontWeight="700">✓ Eligible</text>
              <text x="20" y="89" fontSize="8" fill="#64748B">NSP Scholarship</text>
              <rect x="280" y="80" width="95" height="36" rx="10" fill="#fff" stroke="#BBF7D0" strokeWidth="1.5"/>
              <text x="290" y="96" fontSize="9" fill="#16A34A" fontWeight="700">₹1.25L/year</text>
              <text x="290" y="109" fontSize="8" fill="#64748B">PM Yasasvi</text>
              <rect x="15" y="180" width="85" height="36" rx="10" fill="#fff" stroke="#FDE68A" strokeWidth="1.5"/>
              <text x="25" y="196" fontSize="9" fill="#D97706" fontWeight="700">5 Schemes</text>
              <text x="25" y="209" fontSize="8" fill="#64748B">Found for you</text>
            </svg>
          </div>
        </div>
      </div>

      {/* Stats */}
      <div style={{ background:"#F8FAFF", borderTop:"1px solid #F1F5F9", borderBottom:"1px solid #F1F5F9", padding:"2rem 3rem" }}>
        <div style={{ display:"flex", justifyContent:"center", gap:"5rem", flexWrap:"wrap" }}>
          {stats.map(s => (
            <div key={s.n} style={{ textAlign:"center" }}>
              <div style={{ fontSize:32, fontWeight:800, color:"#2563EB" }}>{s.n}</div>
              <div style={{ fontSize:13, color:"#64748B", marginTop:4 }}>{s.l}</div>
            </div>
          ))}
        </div>
      </div>

      {/* How it works */}
      <div style={{ padding:"5rem 3rem", maxWidth:1100, margin:"0 auto" }}>
        <div style={{ textAlign:"center", marginBottom:"3rem" }}>
          <div style={{ fontSize:13, color:"#2563EB", fontWeight:600, letterSpacing:2, textTransform:"uppercase", marginBottom:8 }}>How It Works</div>
          <div style={{ fontSize:32, fontWeight:800, color:"#0F172A" }}>From profile to opportunity in minutes</div>
        </div>
        <div style={{ display:"grid", gridTemplateColumns:"repeat(auto-fit,minmax(220px,1fr))", gap:20 }}>
          {features.map((f,i) => (
            <div key={i} style={{ background:"#fff", border:"1px solid #F1F5F9", borderRadius:20, padding:"1.75rem", boxShadow:"0 2px 16px rgba(0,0,0,0.04)" }}>
              <div style={{ fontSize:36, marginBottom:12 }}>{f.icon}</div>
              <div style={{ fontWeight:700, fontSize:16, color:"#1E293B", marginBottom:6 }}>{f.title}</div>
              <div style={{ fontSize:13, color:"#64748B", lineHeight:1.7 }}>{f.desc}</div>
            </div>
          ))}
        </div>
      </div>

      {/* Categories */}
      <div style={{ background:"#F8FAFF", padding:"4rem 3rem" }}>
        <div style={{ textAlign:"center", marginBottom:"2.5rem" }}>
          <div style={{ fontSize:28, fontWeight:800, color:"#0F172A", marginBottom:8 }}>Schemes by Category</div>
          <div style={{ color:"#64748B", fontSize:14 }}>All from official Indian government portals</div>
        </div>
        <div style={{ display:"flex", gap:14, justifyContent:"center", flexWrap:"wrap" }}>
          {cats.map(c => (
            <div key={c.label} onClick={onLogin} style={{ background:"#fff", border:`1.5px solid ${c.color=="#F8FAFF"?"#E2E8F0":c.color}`, borderRadius:18, padding:"1.5rem 2rem", cursor:"pointer", textAlign:"center", minWidth:130, boxShadow:"0 2px 12px rgba(0,0,0,0.04)", transition:"all 0.2s" }}>
              <div style={{ fontSize:32, marginBottom:8 }}>{c.icon}</div>
              <div style={{ fontWeight:700, fontSize:14, color:"#1E293B" }}>{c.label}</div>
              <div style={{ fontSize:11, color:c.accent, marginTop:4, fontWeight:600 }}>{c.count}</div>
            </div>
          ))}
        </div>
      </div>

      {/* Who can use */}
      <div style={{ padding:"5rem 3rem", maxWidth:1000, margin:"0 auto" }}>
        <div style={{ textAlign:"center", marginBottom:"2.5rem" }}>
          <div style={{ fontSize:28, fontWeight:800, color:"#0F172A" }}>Who Uses ELIGIFY?</div>
        </div>
        <div style={{ display:"grid", gridTemplateColumns:"repeat(auto-fit,minmax(180px,1fr))", gap:14 }}>
          {[
            { icon:"🧑‍🎓", label:"Students", desc:"Find scholarships matching your category, income & marks" },
            { icon:"👨‍🌾", label:"Farmers", desc:"Discover PM-Kisan and crop insurance benefits" },
            { icon:"👩", label:"Women", desc:"Access girl child schemes, health and welfare programs" },
            { icon:"👨‍👩‍👧", label:"Families", desc:"Map benefits for every member of your household" },
          ].map(p => (
            <div key={p.label} style={{ background:"#fff", border:"1px solid #F1F5F9", borderRadius:18, padding:"1.5rem", textAlign:"center", boxShadow:"0 2px 12px rgba(0,0,0,0.04)" }}>
              <div style={{ fontSize:36, marginBottom:10 }}>{p.icon}</div>
              <div style={{ fontWeight:700, fontSize:15, color:"#1E293B", marginBottom:6 }}>{p.label}</div>
              <div style={{ fontSize:12, color:"#64748B", lineHeight:1.6 }}>{p.desc}</div>
            </div>
          ))}
        </div>
      </div>

      {/* CTA */}
      <div style={{ background:"linear-gradient(135deg,#EFF6FF,#F0FDF4)", borderTop:"1px solid #DBEAFE", padding:"5rem 3rem", textAlign:"center" }}>
        <div style={{ fontSize:32, fontWeight:800, color:"#0F172A", marginBottom:10 }}>Ready to find what you deserve?</div>
        <div style={{ color:"#64748B", fontSize:15, marginBottom:"2rem" }}>Free, private, and takes under 3 minutes to set up.</div>
        <button onClick={onLogin} style={{ padding:"16px 44px", borderRadius:14, border:"none", background:"linear-gradient(135deg,#2563EB,#3B82F6)", color:"#fff", cursor:"pointer", fontSize:17, fontWeight:700, boxShadow:"0 10px 32px rgba(37,99,235,0.25)" }}>
          Check My Eligibility — Free →
        </button>
      </div>

      <div style={{ textAlign:"center", padding:"1.5rem", borderTop:"1px solid #F1F5F9", fontSize:11, color:"#CBD5E1" }}>
        ELIGIFY · All scheme data sourced from official Indian government portals · Not affiliated with any government body
      </div>
    </div>
  );
}

// Shared styles
const inputStyle = {
  width:"100%", boxSizing:"border-box", padding:"10px 12px", borderRadius:10, border:"1.5px solid #E2E8F0", fontSize:13, color:"#1E293B", outline:"none", background:"#fff"
};
const selectStyle = {
  width:"100%", padding:"10px 12px", borderRadius:10, border:"1.5px solid #E2E8F0", fontSize:13, color:"#1E293B", outline:"none", background:"#fff"
};
