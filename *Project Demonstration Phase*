import streamlit as st
from datetime import date

# Set page configuration
st.set_page_config(
    page_title="LegalEase - AI-Powered Legal Document Generator",
    page_icon="⚖️",
    layout="wide"
)

def generate_legal_document(doc_type, details):
    """Generates a structured legal document template based on user inputs."""
    today = date.today().strftime("%B %d, %Y")
    
    if doc_type == "Non-Disclosure Agreement (NDA)":
        return f"""
================================================================================
                         NON-DISCLOSURE AGREEMENT (NDA)
================================================================================

This Non-Disclosure Agreement ("Agreement") is entered into on {today}, by and between:

DISCLOSING PARTY:
  Name: {details.get('disclosing_party', '_________________')}
  Address: {details.get('disclosing_address', '_________________')}

RECEIVING PARTY:
  Name: {details.get('receiving_party', '_________________')}
  Address: {details.get('receiving_address', '_________________')}

1. PURPOSE & CONFIDENTIAL INFORMATION
   The Receiving Party agrees that any technical, business, or operational information 
   disclosed regarding "{details.get('project_scope', 'the Project')}" shall be kept strictly 
   confidential for a duration of {details.get('term_months', 12)} months.

2. OBLIGATIONS
   The Receiving Party shall not disclose, reproduce, or distribute any confidential 
   materials without prior written permission from the Disclosing Party.

3. GOVERNING LAW
   This Agreement shall be governed by and construed under the laws of {details.get('jurisdiction', 'Jurisdiction')}.

IN WITNESS WHEREOF, the parties have executed this Agreement as of the date first written above.

____________________________________            ____________________________________
Disclosing Party Signature                      Receiving Party Signature
"""

    elif doc_type == "Independent Contractor Agreement":
        return f"""
================================================================================
                    INDEPENDENT CONTRACTOR AGREEMENT
================================================================================

This Agreement is made on {today}, between:

CLIENT: {details.get('disclosing_party', '_________________')}
CONTRACTOR: {details.get('receiving_party', '_________________')}

1. SERVICES PROVIDED
   The Contractor agrees to perform the following services:
   "{details.get('project_scope', 'Services description')}"

2. COMPENSATION & PAYMENT
   The Client agrees to pay the Contractor the total sum of ${details.get('payment_amount', '0.00')} 
   upon satisfactory completion of the work.

3. GOVERNING LAW
   This Agreement shall be governed by the laws of {details.get('jurisdiction', 'Jurisdiction')}.

____________________________________            ____________________________________
Client Signature                                Contractor Signature
"""

    return "Please select a valid document type."


# Main UI Header
st.title("⚖️ LegalEase: AI-Powered Legal Document Generator")
st.subheader("Project Demonstration Phase")
st.markdown("---")

# Sidebar - Document Configuration
st.sidebar.header("📋 Document Settings")
doc_type = st.sidebar.selectbox(
    "Select Document Type",
    ["Non-Disclosure Agreement (NDA)", "Independent Contractor Agreement"]
)

st.sidebar.markdown("---")
st.sidebar.subheader("Party Details")
party_a = st.sidebar.text_input("Disclosing Party / Client Name", "Acme Corp")
party_a_addr = st.sidebar.text_input("Disclosing Party Address", "123 Tech Park, Suite 100")

party_b = st.sidebar.text_input("Receiving Party / Contractor Name", "Jane Doe")
party_b_addr = st.sidebar.text_input("Receiving Party Address", "456 Innovation Way")

st.sidebar.markdown("---")
st.sidebar.subheader("Terms & Parameters")
scope = st.sidebar.text_area("Scope / Purpose", "Development of LegalEase AI Platform")
jurisdiction = st.sidebar.selectbox("Jurisdiction / Governing Law", ["California, USA", "New York, USA", "London, UK", "India"])

# Contextual fields based on doc type
additional_details = {
    "disclosing_party": party_a,
    "disclosing_address": party_a_addr,
    "receiving_party": party_b,
    "receiving_address": party_b_addr,
    "project_scope": scope,
    "jurisdiction": jurisdiction,
}

if doc_type == "Non-Disclosure Agreement (NDA)":
    term_months = st.sidebar.slider("Confidentiality Term (Months)", 6, 60, 24)
    additional_details["term_months"] = term_months
elif doc_type == "Independent Contractor Agreement":
    payment = st.sidebar.number_input("Contract Value ($)", min_value=100, value=5000, step=500)
    additional_details["payment_amount"] = payment

# Layout - Main Viewport
col1, col2 = st.columns([1, 1])

with col1:
    st.subheader("🔍 Input Overview")
    st.json({
        "Document Type": doc_type,
        "Party A": party_a,
        "Party B": party_b,
        "Scope": scope,
        "Jurisdiction": jurisdiction
    })
    
    generate_btn = st.button("✨ Generate Document", type="primary", use_container_width=True)

with col2:
    st.subheader("📄 Generated Legal Document Preview")
    
    if generate_btn:
        with st.spinner("Processing template & generating document..."):
            doc_text = generate_legal_document(doc_type, additional_details)
            st.code(doc_text, language="text")
            
            # Download Option
            st.download_button(
                label="📥 Download Document (.txt)",
                data=doc_text,
                file_name=f"{doc_type.replace(' ', '_')}.txt",
                mime="text/plain",
                use_container_width=True
            )
    else:
        st.info("Click **Generate Document** to view the live preview.")
