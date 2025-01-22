# jobby-app-repository

jobby-app/

jobby-app/
├── src/
│   ├── components/
│   │   ├── Header/
│   │   │   ├── index.js  
│   │   │   └── index.css
│   │   ├── Home/
│   │   │   ├── index.js
│   │   │   └── index.css
│   │   ├── JobCard/
│   │   │   ├── index.js
│   │   │   └── index.css
│   │   ├── JobDetails/
│   │   │   ├── index.js
│   │   │   └── index.css
│   │   ├── Jobs/
│   │   │   ├── index.js
│   │   │   └── index.css
│   │   └── LoginForm/
│   │   │   ├── index.js
│   │   │   └── index.css
│   │   ├── NotFound/
│   │   │   ├── index.js
│   │   │   └── index.css
│   │   ├── Profile/
│   │   │   ├── index.js
│   │   │   └── index.css
│   │   ├── ProtectedRoute/
│   │   │   ├── index.js
│   │   │   └── index.css
│   │   ├── SimilarJobItem/
│   │       ├── index.js
│   │       └── index.css
│   ├── index.js
│   ├── App.js
│   └── App.css


                                                                        #Header /index.js

import {Component} from 'react'
import {Link, withRouter} from 'react-router-dom'
import Cookies from 'js-cookie'
import './index.css'

class Header extends Component {
  onClickWebsiteLogo = () => {
    const {history} = this.props // Use `this.props` to access the history object
    history.replace('/') // Redirect to the home page
  }

  onClickLogout = () => {
    const {history} = this.props // Use `this.props` to access the history object
    Cookies.remove('jwt_token')
    history.replace('/login') // Redirect to the login page
  }
  render() {
    return (
      <div className="header">
        <div className="header-content">
          <Link to="/" className="header-logo-link">
            <img
              src="https://assets.ccbp.in/frontend/react-js/logo-img.png"
              alt="website logo"
              className="header-logo"
            />
          </Link>
          <nav className="nav-links">
            <ul className="nav-list">
              <li className="nav-item">
                <Link to="/" className="nav-link">
                  Home
                </Link>
              </li>
              <li className="nav-item">
                <Link to="/jobs" className="nav-link">
                  Jobs
                </Link>
              </li>
              <li className="nav-item">
                <button
                  type="button"
                  className="logout-button"
                  onClick={this.onClickLogout}
                >
                  LogOut
                </button>
              </li>
            </ul>
          </nav>
        </div>
      </div>
    )
  }
}

export default withRouter(Header)


                                                                            #Header /index.css 


.header {
  display: flex;
  justify-content: center;
  background-color: #1c1c2b;
  padding: 15px 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  max-width: 1200px;
}


.header-logo {
  height: 50px; 
  width: auto;
}

.header-logo-link {
  text-decoration: none; 
}

/* Navigation Styling */
.nav-links {
  display: flex;
  align-items: center;
}

.nav-list {
  list-style-type: none;
  display: flex;
  margin: 0;
  padding: 0;
  gap: 20px; 
}

.nav-item {
  display: flex;
  align-items: center;
}

.nav-link {
  text-decoration: none; 
  color: #ffffff; 
  font-size: 16px;
  font-weight: 500;
  transition: color 0.3s ease; 
}

.nav-link:hover {
  color: #2cc6c6; 
}

/* Logout Button */
.logout-button {
  background-color: transparent; 
  border: 1px solid #ffffff;
  color: #ffffff;
  padding: 6px 12px;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.logout-button:hover {
  background-color: #ffffff;
  color: #1c1c2b; 
}

/* Responsive Design */
@media (max-width: 768px) {
  .header-content {
    flex-direction: column; 
    align-items: center;
  }

  .nav-list {
    flex-direction: column;
    align-items: center;
    gap: 10px;
    margin-top: 10px;
  }

  .nav-item {
    margin: 0;
  }

  .logout-button {
    font-size: 12px; /* Adjust font size for smaller screens */
    padding: 5px 10px;
  }
}

@media (min-width: 1200px) {
  .header-content {
    max-width: 1400px; /* Expand for larger screens */
  }
}



                                                                 #Home /index.js

import {Component} from 'react'
import {Redirect, withRouter, Link} from 'react-router-dom'
import Cookies from 'js-cookie'
import Header from '../Header'
import './index.css'

class Home extends Component {
  onClickToJobs = () => {
    const {history} = this.props
    history.push('/jobs')
  }
  render() {
    const jwtToken = Cookies.get('jwt_token')
    if (jwtToken === undefined) {
      return <Redirect to="/login" /> // Redirect to login if no token is found
    }

    return (
      <div>
        <Header />
        <div className="home-container">
          <h1 className="home-heading">
            Find The Job That <br />
            Fits Your Life
          </h1>
          <p className="home-paragraph">
            Millions of people are searching for jobs, salary <br />
            information, company reviews.Find the job that fits your <br />
            abilities and potential
          </p>
          <Link to="/jobs">
            <button type="button" className="home-button">
              Find Jobs
            </button>
          </Link>
        </div>
      </div>
    )
  }
}

export default withRouter(Home)

                                                                      #Home ./index.css 


.home-container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  background-image: url('https://assets.ccbp.in/frontend/react-js/home-sm-bg.png');
  background-size: cover;
  background-position: center;
  color: #ffffff;
  padding: 40px 20px;
  height: 100vh;
  text-align: center;
}

/* Heading styling */
.home-heading {
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 16px;
}

/* Paragraph styling */
.home-paragraph {
  font-size: 16px;
  margin-bottom: 24px;
  max-width: 700px;
}

/* Button styling */
.home-button {
  background-color: #2cc6c6;
  border: none;
  color: #ffffff;
  font-size: 16px;
  padding: 12px 24px;
  cursor: pointer;
  border-radius: 4px;
  transition: background-color 0.3s;
}

.home-button:hover {
  background-color: #1fa0a0;
}

/* Extra Small Screens (less than 576px) */
@media (max-width: 575px) {
  .home-container {
    background-image: url('https://assets.ccbp.in/frontend/react-js/home-sm-bg.png');
    background-size: cover;
  }

  .home-heading {
    font-size: 24px;
  }

  .home-paragraph {
    font-size: 14px;
  }

  .home-button {
    font-size: 14px;
    padding: 10px 20px;
  }
}

/* Small Screens (576px to 767px) */
@media (min-width: 576px) and (max-width: 767px) {
  .home-container {
    background-image: url('https://assets.ccbp.in/frontend/react-js/home-sm-bg.png');
    background-size: cover;
  }

  .home-heading {
    font-size: 26px;
  }

  .home-paragraph {
    font-size: 15px;
  }

  .home-button {
    font-size: 15px;
    padding: 12px 22px;
  }
}

/* Medium Screens (768px to 991px) */
@media (min-width: 768px) and (max-width: 991px) {
  .home-container {
    background-image: url('https://assets.ccbp.in/frontend/react-js/home-lg-bg.png');
    background-size: cover;
  }

  .home-heading {
    font-size: 32px;
  }

  .home-paragraph {
    font-size: 18px;
  }

  .home-button {
    font-size: 18px;
    padding: 14px 28px;
  }
}

/* Large Screens (992px and above) */
@media (min-width: 992px) {
  .home-container {
    background-image: url('https://assets.ccbp.in/frontend/react-js/home-lg-bg.png');
    background-size: cover;
  }

  .home-heading {
    font-size: 36px;
  }

  .home-paragraph {
    font-size: 20px;
  }

  .home-button {
    font-size: 20px;
    padding: 16px 32px;
  }
}


                                                                   #JobCard  /index.js

import React from 'react'
import {Link} from 'react-router-dom'
import {FaStar, FaMapMarkerAlt, FaSuitcase} from 'react-icons/fa' // Import icons
import './index.css'

const JobCard = props => {
  const {jobDetails} = props

  const {
    id,
    companyLogoUrl,
    employmentType,
    jobDescription,
    location,
    packagePerAnnum,
    rating,
    title, // Fixed typo from `tittle` to `title`
  } = jobDetails

  return (
    <Link to={`/jobs/${id}`}>
      <li className="job-card">
        <div className="job-card-header">
          <img
            src={companyLogoUrl}
            alt="company logo"
            className="company-logo"
          />
          <div className="job-card-header-details">
            <h1 className="job-title">{title}</h1>
            <div className="job-rating">
              <FaStar className="rating-icon" />
              <p className="rating">{rating}</p>
            </div>
          </div>
        </div>
        <div className="job-card-info">
          <div className="job-location">
            <FaMapMarkerAlt className="info-icon" />
            <p className="info-text">{location}</p>
          </div>
          <div className="job-employment">
            <FaSuitcase className="info-icon" />
            <p className="info-text">{employmentType}</p>
          </div>
          <p className="job-salary">{packagePerAnnum} LPA</p>
        </div>
        <hr className="separator" />
        <div className="job-description">
          <h1 className="description-heading">Description</h1>
          <p className="description-text">{jobDescription}</p>
        </div>
      </li>
    </Link>
  )
}

export default JobCard

                                                                    #JobCard  /index.css

.job-card {
  background-color: #1f1f2f; 
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
  color: #ffffff; /* White text for readability */
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.4); 
}

.job-card-header {
  display: flex;
  align-items: center;
  margin-bottom: 16px;
}

.company-logo {
  width: 50px;
  height: 50px;
  border-radius: 4px; 
  margin-right: 16px;
}

.job-card-header-details {
  display: flex;
  flex-direction: column;
}

.job-title {
  font-size: 20px;
  font-weight: 600;
  color: #e2e8f0; /* Light text color */
  margin-bottom: 8px;
}

.job-rating {
  display: flex;
  align-items: center;
}

.rating-icon {
  color: #fbbf24; 
  margin-right: 8px;
}

.rating {
  font-size: 16px;
  color: #94a3b8; 
}

.job-card-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap; /* Ensures proper alignment on smaller screens */
  margin-bottom: 16px;
}

.job-location,
.job-employment {
  display: flex;
  align-items: center;
  margin-right: 20px; 
}

.info-icon {
  color: #64748b; /* Subtle icon color */
  margin-right: 8px;
}

.info-text {
  font-size: 16px;
  color: #cbd5e1; /* Muted text color */
}

.job-salary {
  font-size: 16px;
  font-weight: bold;
  color: #2cc6c6; 
}

.separator {
  border: 1px solid #2c2c3e; 
  margin: 16px 0;
}

.job-description {
  display: flex;
  flex-direction: column;
}

.description-heading {
  font-size: 18px;
  font-weight: bold;
  color: #e2e8f0; 
  margin-bottom: 8px;
}

.description-text {
  font-size: 14px;
  color: #94a3b8; 
  line-height: 1.6;
}

/* Additional Styling for a Clean Layout */
.job-card-info .job-salary {
  margin-left: auto; 
}

.job-card-header,
.job-card-info {
  gap: 12px; 
}

                                                                  #JobDetails ./index.js
                                                              
import {Component} from 'react'
import Cookies from 'js-cookie'
import Loader from 'react-loader-spinner'
import {BsArrowLeftShort} from 'react-icons/bs'
import SimilarJobItem from '../SimilarJobItem'
import './index.css'

const apiStatusConstants = {
  initial: 'INITIAL',
  inProgress: 'IN_PROGRESS',
  success: 'SUCCESS',
  failure: 'FAILURE',
}

class JobDetails extends Component {
  state = {
    jobDetails: {},
    similarJobs: [],
    apiStatus: apiStatusConstants.initial,
  }

  componentDidMount() {
    this.getJobDetails()
  }

  getJobDetails = async () => {
    this.setState({apiStatus: apiStatusConstants.inProgress})
    const {match} = this.props
    const {params} = match
    const {id} = params
    const jwtToken = Cookies.get('jwt_token')
    const apiUrl = `https://apis.ccbp.in/jobs/${id}`
    const options = {
      method: 'GET',
      headers: {
        Authorization: `Bearer ${jwtToken}`,
      },
    }
    const response = await fetch(apiUrl, options)
    if (response.ok === true) {
      const fetchedData = await response.json()
      const updatedJobDetails = {
        companyLogoUrl: fetchedData.job_details.company_logo_url,
        companyWebsiteUrl: fetchedData.job_details.company_website_url,
        employmentType: fetchedData.job_details.employment_type,
        id: fetchedData.job_details.id,
        jobDescription: fetchedData.job_details.job_description,
        location: fetchedData.job_details.location,
        packagePerAnnum: fetchedData.job_details.package_per_annum,
        rating: fetchedData.job_details.rating,
        title: fetchedData.job_details.title,
        skills: fetchedData.job_details.skills.map(skill => ({
          imageUrl: skill.image_url,
          name: skill.name,
        })),
        lifeAtCompany: {
          description: fetchedData.job_details.life_at_company.description,
          imageUrl: fetchedData.job_details.life_at_company.image_url,
        },
      }

      const updatedSimilarJobs = fetchedData.similar_jobs.map(job => ({
        id: job.id,
        companyLogoUrl: job.company_logo_url,
        employmentType: job.employment_type,
        jobDescription: job.job_description,
        location: job.location,
        rating: job.rating,
        title: job.title,
      }))

      this.setState({
        jobDetails: updatedJobDetails,
        similarJobs: updatedSimilarJobs,
        apiStatus: apiStatusConstants.success,
      })
    } else {
      this.setState({apiStatus: apiStatusConstants.failure})
    }
  }

  renderLoader = () => (
    <div data-testid="loader" className="loader-container">
      <Loader type="ThreeDots" color="#0b69ff" height={80} width={80} />
    </div>
  )

  renderFailureView = () => (
    <div className="failure-view-container">
      <img
        src="https://assets.ccbp.in/frontend/react-js/failure-img.png"
        alt="failure view"
        className="failure-view-image"
      />
      <h1 className="failure-view-heading">Oops! Something Went Wrong</h1>
      <p>We cannot seem to find the page you are looking for</p>
      <button
        type="button"
        className="retry-button"
        onClick={this.getJobDetails}
      >
        Retry
      </button>
    </div>
  )

  renderJobDetails = () => {
    const {jobDetails, similarJobs} = this.state
    const {
      companyLogoUrl,
      companyWebsiteUrl,
      employmentType,
      jobDescription,
      location,
      packagePerAnnum,
      rating,
      title,
      skills,
      lifeAtCompany,
    } = jobDetails

    return (
      <div className="job-details-success-view">
        <div className="job-details-container">
          <div className="job-header">
            <img
              src={companyLogoUrl}
              alt="job details company logo"
              className="company-logo"
            />
            <div className="job-title-container">
              <h1 className="job-title">{title}</h1>
              <p className="job-rating">
                <span className="rating-icon">⭐</span> {rating}
              </p>
            </div>
          </div>
          <div className="job-info">
            <p className="job-location">{location}</p>
            <p className="job-employment-type">{employmentType}</p>
            <p className="job-package">{packagePerAnnum}</p>
          </div>
          <hr />
          <h2 className="job-description-heading">Description</h2>
          <p className="job-description">{jobDescription}</p>
          <a
            href={companyWebsiteUrl}
            target="_blank"
            rel="noopener noreferrer"
            className="company-website-link"
          >
            Visit Company Website
          </a>
          <hr />
          <h1 className="skills-heading">Skills</h1>
          <ul className="skills-list">
            {skills.map(skill => (
              <li key={skill.name} className="skill-item">
                <img
                  src={skill.imageUrl}
                  alt={skill.name}
                  className="skill-icon"
                />
                <h1>{skill.name}</h1>
              </li>
            ))}
          </ul>
          <hr />
          <h2 className="life-at-company-heading">Life at Company</h2>
          <div className="life-at-company">
            <p>{lifeAtCompany.description}</p>
            <img
              src={lifeAtCompany.imageUrl}
              alt="life at company"
              className="life-at-company-image"
            />
          </div>
        </div>
        <h1 className="similar-jobs-heading">Similar Jobs</h1>
        <ul className="similar-jobs-list">
          {similarJobs.map(job => (
            <SimilarJobItem key={job.id} jobDetails={job} />
          ))}
        </ul>
      </div>
    )
  }

  renderJobDetailsView = () => {
    const {apiStatus} = this.state

    switch (apiStatus) {
      case apiStatusConstants.success:
        return this.renderJobDetails()
      case apiStatusConstants.failure:
        return this.renderFailureView()
      case apiStatusConstants.inProgress:
        return this.renderLoader()
      default:
        return null
    }
  }

  render() {
    return (
      <div className="job-details-page">
        <button
          type="button"
          className="back-button"
          onClick={() => this.props.history.goBack()}
        >
          <BsArrowLeftShort size={24} />
        </button>
        {this.renderJobDetailsView()}
      </div>
    )
  }
}

export default JobDetails
                                                                  #JobDetails ./index.css
.job-details-page {
  background-color: #1a1a1a;
  color: #ffffff;
  font-family: 'Arial', sans-serif;
  min-height: 100vh;
  padding: 20px;
}


.back-button {
  display: flex;
  align-items: center;
  background-color: transparent;
  border: none;
  color: #ffffff;
  cursor: pointer;
  margin-bottom: 20px;
}

.back-button:hover {
  color: #fbc02d;
}

/* Job Details Section */
.job-details-container {
  background-color: #262626;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

/* Header - Company Logo and Title */
.job-header {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 20px;
}

.company-logo {
  width: 60px;
  height: 60px;
  border-radius: 8px;
}

.job-title-container {
  display: flex;
  flex-direction: column;
}

.job-title {
  font-size: 24px;
  font-weight: bold;
}

.job-rating {
  display: flex;
  align-items: center;
  font-size: 16px;
  color: #fbc02d;
}

.rating-icon {
  margin-right: 5px;
}

/* Job Info Section */
.job-info {
  display: flex;
  gap: 20px;
  margin-bottom: 20px;
  font-size: 14px;
}

.job-location,
.job-employment-type,
.job-package {
  background-color: #333333;
  padding: 5px 10px;
  border-radius: 4px;
}

/* Description and Skills Section */
.job-description-heading,
.skills-heading,
.life-at-company-heading,
.similar-jobs-heading {
  font-size: 20px;
  margin-bottom: 10px;
  color: #fbc02d;
}

.job-description {
  margin-bottom: 20px;
}

.company-website-link {
  color: #0b69ff;
  text-decoration: none;
  font-size: 14px;
}

.company-website-link:hover {
  text-decoration: underline;
}

/* Skills Section */
.skills-list {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  margin-bottom: 20px;
}

.skill-item {
  display: flex;
  align-items: center;
  gap: 10px;
  background-color: #333333;
  padding: 10px;
  border-radius: 4px;
}

.skill-icon {
  width: 30px;
  height: 30px;
  border-radius: 4px;
}

/* Life at Company Section */
.life-at-company {
  display: flex;
  align-items: center;
  gap: 20px;
  margin-bottom: 20px;
}

.life-at-company-image {
  width: 150px;
  height: 150px;
  border-radius: 8px;
  object-fit: cover;
}

/* Similar Jobs Section */
.similar-jobs-heading {
  margin-top: 30px;
  margin-bottom: 15px;
}

.similar-jobs-list {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  list-style-type: none;
  padding: 0;
}

/* Loader Styling */
.loader-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50vh;
}

/* Failure View Styling */
.failure-view-container {
  text-align: center;
  padding: 20px;
}

.failure-view-image {
  width: 200px;
  margin-bottom: 20px;
}

.failure-view-heading {
  font-size: 18px;
  margin-bottom: 20px;
}

.retry-button {
  padding: 10px 20px;
  background-color: #0b69ff;
  color: #ffffff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.retry-button:hover {
  background-color: #0353e9;
}

                                                                       #Jobs ./index.js
 import {Component} from 'react'
import Cookies from 'js-cookie'
import Loader from 'react-loader-spinner'
import JobCard from '../JobCard'
import Header from '../Header'
import Profile from '../Profile'

import './index.css'

const apiStatusConstants = {
  initial: 'INITIAL',
  success: 'SUCCESS',
  failure: 'FAILURE',
  inProgress: 'IN_PROGRESS',
}

// These are the lists used in the application.

const employmentTypesList = [
  {label: 'Full Time', employmentTypeId: 'FULLTIME'},
  {label: 'Part Time', employmentTypeId: 'PARTTIME'},
  {label: 'Freelance', employmentTypeId: 'FREELANCE'},
  {label: 'Internship', employmentTypeId: 'INTERNSHIP'},
]

const salaryRangesList = [
  {salaryRangeId: '1000000', label: '10 LPA and above'},
  {salaryRangeId: '2000000', label: '20 LPA and above'},
  {salaryRangeId: '3000000', label: '30 LPA and above'},
  {salaryRangeId: '4000000', label: '40 LPA and above'},
]

class Jobs extends Component {
  state = {
    jobsList: [],
    apiStatus: apiStatusConstants.initial,
    searchInput: '',
    activeEmploymentTypeId: '',
    activeSalaryRangeId: '',
  }

  componentDidMount() {
    this.getJobDetails()
  }

  getJobDetails = async () => {
    this.setState({apiStatus: apiStatusConstants.inProgress})
    const jwtToken = Cookies.get('jwt_token')
    const {activeEmploymentTypeId, activeSalaryRangeId, searchInput} =
      this.state
    const apiUrl = `https://apis.ccbp.in/jobs?employment_type=${activeEmploymentTypeId}&minimum_package=${activeSalaryRangeId}&search=${searchInput}`
    const options = {
      headers: {
        Authorization: `Bearer ${jwtToken}`,
      },
      method: 'GET',
    }

    const response = await fetch(apiUrl, options)
    if (response.ok) {
      const fetchedData = await response.json()
      const updatedData = fetchedData.jobs.map(job => ({
        companyLogoUrl: job.company_logo_url,
        employmentType: job.employment_type,
        id: job.id,
        jobDescription: job.job_description,
        location: job.location,
        packagePerAnnum: job.package_per_annum,
        rating: job.rating,
        title: job.title,
      }))
      this.setState({
        jobsList: updatedData,
        apiStatus: apiStatusConstants.success,
      })
    } else {
      this.setState({apiStatus: apiStatusConstants.failure})
    }
  }

  changeSearchInput = event => {
    this.setState({searchInput: event.target.value})
  }

  enterSearchInput = () => {
    this.getJobDetails()
  }

  updateActiveEmploymentType = employmentTypeId => {
    this.setState(
      {activeEmploymentTypeId: employmentTypeId},
      this.getJobDetails,
    )
  }

  updateActiveSalaryRange = salaryRangeId => {
    this.setState({activeSalaryRangeId: salaryRangeId}, this.getJobDetails)
  }

  renderFailureView = () => (
    <div className="jobs-error-view-container">
      <img
        src="https://assets.ccbp.in/frontend/react-js/failure-img.png"
        alt="failure view"
        className="jobs-failure-img"
      />
      <h1 className="jobs-failure-heading-text">Oops! Something Went Wrong</h1>
      <p className="jobs-failure-description">
        We are having some trouble processing your request. Please try again.
      </p>
    </div>
  )

  renderLoadingView = () => (
    <div className="jobs-loader-container" data-testid="loader">
      <Loader type="ThreeDots" color="#0b69ff" height="50" width="50" />
    </div>
  )

  renderJobsListView = () => {
    const {jobsList} = this.state

    const shouldShowJobsList = jobsList.length > 0

    return shouldShowJobsList ? (
      <ul className="jobs-list">
        {jobsList.map(job => (
          <JobCard jobDetails={job} key={job.id} />
        ))}
      </ul>
    ) : (
      <div className="no-jobs-view">
        <img
          src="https://assets.ccbp.in/frontend/react-js/no-jobs-img.png"
          alt="no jobs"
          className="no-jobs-img"
        />
        <h1 className="no-jobs-heading">No Jobs Found</h1>
        <p className="no-jobs-description">
          We could not find any jobs. Try other filters.
        </p>
      </div>
    )
  }

  renderAllJobs = () => {
    const {apiStatus} = this.state

    switch (apiStatus) {
      case apiStatusConstants.success:
        return this.renderJobsListView()
      case apiStatusConstants.failure:
        return this.renderFailureView()
      case apiStatusConstants.inProgress:
        return this.renderLoadingView()
      default:
        return null
    }
  }

  renderFilters = () => (
    <div className="filters-group-container">
      <Profile />
      <h1 className="filters-heading">Type of Employment</h1>
      <ul className="filters-list">
        {employmentTypesList.map(type => (
          <li key={type.employmentTypeId}>
            <input
              type="checkbox"
              id={type.employmentTypeId}
              onChange={() =>
                this.updateActiveEmploymentType(type.employmentTypeId)
              }
            />
            <label htmlFor={type.employmentTypeId} className="filter-label">
              {type.label}
            </label>
          </li>
        ))}
      </ul>
      <h1 className="filters-heading">Salary Range</h1>
      <ul className="filters-list">
        {salaryRangesList.map(range => (
          <li key={range.salaryRangeId}>
            <input
              type="radio"
              id={range.salaryRangeId}
              name="salary"
              onChange={() => this.updateActiveSalaryRange(range.salaryRangeId)}
            />
            <label htmlFor={range.salaryRangeId} className="filter-label">
              {range.label}
            </label>
          </li>
        ))}
      </ul>
    </div>
  )

  render() {
    const {searchInput} = this.state

    return (
      <div className="jobs-container">
        <Header />
        <div className="jobs-content">
          {this.renderFilters()}
          <div className="jobs-section">
            <div className="search-container">
              <input
                type="search"
                value={searchInput}
                onChange={this.changeSearchInput}
                placeholder="Search"
                className="search-input"
              />
              <button
                data-testid="searchButton"
                type="button"
                onClick={this.enterSearchInput}
                className="search-button"
              >
                <img
                  src="https://assets.ccbp.in/frontend/react-js/search-icon.png"
                  alt="search icon"
                  className="search-icon"
                />
              </button>
            </div>
            {this.renderAllJobs()}
          </div>
        </div>
      </div>
    )
  }
}

export default Jobs
                                                                    #Jobs ./index.css                                                                 
                                                                    
.jobs-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background-color: #f1f5f9;
  font-family: 'Roboto', sans-serif;
}

.jobs-content {
  display: flex;
  flex: 1;
  padding: 20px;
  gap: 20px;
}

.filters-group-container {
  width: 20%;
  background-color: #ffffff;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
}

.filters-heading {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 16px;
  color: #334155;
}

.filters-list {
  list-style-type: none;
  padding: 0;
  margin: 0 0 20px 0;
}

.filter-label {
  margin-left: 8px;
  color: #475569;
  font-size: 16px;
  cursor: pointer;
}

.jobs-section {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.search-container {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.search-input {
  flex: 1;
  height: 36px;
  padding: 8px;
  border: 1px solid #cbd5e1;
  border-radius: 4px;
  outline: none;
  font-size: 14px;
}

.search-button {
  background-color: transparent;
  border: none;
  margin-left: 8px;
  cursor: pointer;
}

.search-icon {
  width: 20px;
  height: 20px;
}

.jobs-loader-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.jobs-error-view-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
  text-align: center;
}

.jobs-failure-img {
  width: 200px;
  margin-bottom: 16px;
}

.jobs-failure-heading-text {
  font-size: 24px;
  font-weight: bold;
  color: #475569;
  margin-bottom: 8px;
}

.jobs-failure-description {
  font-size: 16px;
  color: #64748b;
}

.no-jobs-view {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  margin-top: 50px;
}

.no-jobs-img {
  width: 150px;
  margin-bottom: 16px;
}

.no-jobs-heading {
  font-size: 24px;
  font-weight: bold;
  color: #475569;
  margin-bottom: 8px;
}

.no-jobs-description {
  font-size: 16px;
  color: #64748b;
}

.jobs-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
}
                                                                 #LoginForm ./index.js
import {Component} from 'react'
import {Redirect} from 'react-router-dom'
import Cookies from 'js-cookie'
import './index.css'

class LoginForm extends Component {
  state = {
    username: '',
    password: '',
    showSubmitError: false,
    errorMsg: '',
  }

  onChangeUsername = event => {
    this.setState({username: event.target.value})
  }

  onChangePassword = event => {
    this.setState({password: event.target.value})
  }

  onSubmitSuccess = jwtToken => {
    const {history} = this.props
    Cookies.set('jwt_token', jwtToken, {
      expires: 30,
      path: '/',
    })
    history.replace('/')
  }

  onSubmitFailure = errorMsg => {
    this.setState({showSubmitError: true, errorMsg})
  }

  submitForm = async event => {
    event.preventDefault()
    const {username, password} = this.state
    const userDetails = {username, password}
    const url = 'https://apis.ccbp.in/login'
    const options = {
      method: 'POST',
      body: JSON.stringify(userDetails),
    }

    const response = await fetch(url, options)
    const data = await response.json()

    if (response.ok) {
      this.onSubmitSuccess(data.jwt_token)
    } else {
      this.onSubmitFailure(data.error_msg)
    }
  }

  renderPasswordField = () => {
    const {password} = this.state
    return (
      <>
        <label className="input-label" htmlFor="password">
          PASSWORD
        </label>
        <input
          type="password"
          id="password"
          className="password-input-field"
          value={password}
          placeholder="rahul@2021"
          onChange={this.onChangePassword}
        />
      </>
    )
  }

  renderUsernameField = () => {
    const {username} = this.state
    return (
      <>
        <label className="input-label" htmlFor="username">
          USERNAME
        </label>
        <input
          type="text"
          id="username"
          className="username-input-field"
          value={username}
          placeholder="rahul"
          onChange={this.onChangeUsername}
        />
      </>
    )
  }

  render() {
    const {showSubmitError, errorMsg} = this.state
    const jwtToken = Cookies.get('jwt_token')
    if (jwtToken) {
      return <Redirect to="/" />
    }
    return (
      <div className="login-form-container">
        <form className="form-container" onSubmit={this.submitForm}>
          <img
            src="https://assets.ccbp.in/frontend/react-js/logo-img.png"
            alt="website logo"
            className="login-website-logo-desktop-image"
          />
          <div className="input-container">{this.renderUsernameField()}</div>
          <div className="input-container">{this.renderPasswordField()}</div>
          <button type="submit" className="login-button">
            Login
          </button>
          {showSubmitError && <p className="error-message">*{errorMsg}</p>}
        </form>
      </div>
    )
  }
}

export default LoginForm
                                                             #LoginForm ./index.css
.login-form-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f8f9fa; /* Light background for contrast */
  font-family: 'Roboto', sans-serif;
  padding: 16px;
  box-sizing: border-box;
}

.form-container {
  background-color: #ffffff;
  width: 100%;
  max-width: 400px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  padding: 24px 32px;
  box-sizing: border-box;
}

.login-website-logo-desktop-image {
  display: block;
  margin: 0 auto 24px;
  width: 150px;
}

.input-container {
  margin-bottom: 16px;
}

.input-label {
  font-size: 14px;
  font-weight: 500;
  color: #495057;
  margin-bottom: 8px;
  display: block;
}

.username-input-field,
.password-input-field {
  width: 100%;
  padding: 12px;
  font-size: 14px;
  color: #495057;
  border: 1px solid #ced4da;
  border-radius: 4px;
  outline: none;
  box-sizing: border-box;
}

.username-input-field:focus,
.password-input-field:focus {
  border-color: #2d87bb;
  box-shadow: 0 0 4px rgba(45, 135, 187, 0.3);
}

.login-button {
  width: 100%;
  padding: 12px;
  font-size: 16px;
  font-weight: bold;
  color: #ffffff;
  background-color: #2d87bb;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.login-button:hover {
  background-color: #256a98;
}

.error-message {
  font-size: 12px;
  color: #f54394;
  margin-top: 8px;
  text-align: center;
}

/* Extra Small and Small Screens (less than 768px) */
@media (max-width: 575px) {
  .form-container {
    padding: 16px 20px;
  }

  .login-website-logo-desktop-image {
    width: 120px;
  }

  .username-input-field,
  .password-input-field {
    padding: 10px;
  }

  .login-button {
    font-size: 14px;
    padding: 10px;
  }
}

/* Small Screens (576px to 767px) */
@media (min-width: 576px) and (max-width: 767px) {
  .form-container {
    padding: 20px 28px;
  }

  .login-website-logo-desktop-image {
    width: 130px;
  }

  .username-input-field,
  .password-input-field {
    padding: 12px;
  }

  .login-button {
    font-size: 15px;
  }
}

/* Medium Screens (768px and above) */
@media (min-width: 768px) {
  .form-container {
    max-width: 450px;
    padding: 32px 40px;
  }

  .login-website-logo-desktop-image {
    width: 160px;
  }

  .username-input-field,
  .password-input-field {
    font-size: 16px;
    padding: 14px;
  }

  .login-button {
    font-size: 18px;
    padding: 14px;
  }
}

/* Large and Extra Large Screens (992px and above) */
@media (min-width: 992px) {
  .form-container {
    max-width: 500px;
    padding: 40px 50px;
  }

  .login-website-logo-desktop-image {
    width: 180px;
  }

  .username-input-field,
  .password-input-field {
    font-size: 18px;
  }

  .login-button {
    font-size: 20px;
  }
}

/* Failure View Specific Styles */
@media (min-width: 768px) {
  .error-message {
    font-size: 14px;
    margin-top: 12px;
    color: #dc3545; /* Bright red for better visibility */
  }
}

                                                                   #NotFound index.js 
const NotFound = () => (
  <div className="not-found-container">
    <img
      src="https://assets.ccbp.in/frontend/react-js/jobby-app-not-found-img.png"
      alt="not found"
      className="not-found-img"
    />
    <h1>Page Not Found</h1>
    <p>we're sorry, the page you requested could not be found</p>
  </div>
)

export default NotFound

                                                                   #Profile ./index.js
import {Component} from 'react'
import Cookies from 'js-cookie'
import Loader from 'react-loader-spinner'
import './index.css'

const apiStatusConstants = {
  initial: 'INITIAL',
  success: 'SUCCESS',
  failure: 'FAILURE',
  inProgress: 'IN_PROGRESS',
}

class Profile extends Component {
  state = {
    profileDetails: {},
    apiStatus: apiStatusConstants.initial,
  }

  componentDidMount() {
    this.getProfileDetails()
  }

  getProfileDetails = async () => {
    this.setState({apiStatus: apiStatusConstants.inProgress})
    const jwtToken = Cookies.get('jwt_token')
    const apiUrl = 'https://apis.ccbp.in/profile'
    const options = {
      headers: {
        Authorization: `Bearer ${jwtToken}`,
      },
      method: 'GET',
    }

    const response = await fetch(apiUrl, options)
    if (response.ok) {
      const fetchedData = await response.json()
      const updatedData = {
        name: fetchedData.profile_details.name,
        profileImageUrl: fetchedData.profile_details.profile_image_url,
        shortBio: fetchedData.profile_details.short_bio,
      }
      this.setState({
        profileDetails: updatedData,
        apiStatus: apiStatusConstants.success,
      })
    } else {
      this.setState({apiStatus: apiStatusConstants.failure})
    }
  }

  renderProfileDetails = () => {
    const {profileDetails} = this.state
    const {name, profileImageUrl, shortBio} = profileDetails

    return (
      <div className="profile-container">
        <img src={profileImageUrl} alt="profile" className="profile-image" />
        <h1 className="profile-name">{name}</h1>
        <p className="profile-bio">{shortBio}</p>
      </div>
    )
  }

  renderFailureView = () => (
    <div className="profile-error-view">
      <p className="profile-error-message">
        Failed to fetch profile details. Please try again.
      </p>
      <button
        type="button"
        className="retry-button"
        onClick={this.getProfileDetails}
      >
        Retry
      </button>
    </div>
  )

  renderLoadingView = () => (
    <div className="profile-loader" data-testid="loader">
      <Loader type="ThreeDots" color="#0b69ff" height="50" width="50" />
    </div>
  )

  renderProfileView = () => {
    const {apiStatus} = this.state

    switch (apiStatus) {
      case apiStatusConstants.success:
        return this.renderProfileDetails()
      case apiStatusConstants.failure:
        return this.renderFailureView()
      case apiStatusConstants.inProgress:
        return this.renderLoadingView()
      default:
        return null
    }
  }

  render() {
    return <div className="profile-section">{this.renderProfileView()}</div>
  }
}

export default Profile

                                                             #profile ./index.css
.profile-section {
  padding: 20px;
  background-color: #f1f5f9;
  border-radius: 8px;
  text-align: center;
}

.profile-image {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  margin-bottom: 12px;
}

.profile-name {
  font-size: 18px;
  font-weight: bold;
  color: #334155;
  margin-bottom: 8px;
}

.profile-bio {
  font-size: 14px;
  color: #475569;
}

.profile-error-view {
  text-align: center;
}

.profile-error-message {
  color: #ff0000;
  font-size: 14px;
  margin-bottom: 8px;
}

.retry-button {
  background-color: #0b69ff;
  color: #ffffff;
  border: none;
  padding: 8px 12px;
  border-radius: 4px;
  cursor: pointer;
}



                                                             #ProtectedRoute ./index.js 
import {Redirect, Route} from 'react-router-dom'
import Cookie from 'js-cookie'

const ProtectedRoute = props => {
  const token = Cookie.get('jwt_token')
  if (token === undefined) {
    return <Redirect to="/login" />
  }
  return <Route {...props} />
}

export default ProtectedRoute


                                                             #SimilarJobItem ./index.js
  import React from 'react'
import {FaStar, FaMapMarkerAlt, FaSuitcase} from 'react-icons/fa' // Import icons
import './index.css'

const SimilarJobItem = props => {
  const {jobDetails} = props
  const {
    id,
    companyLogoUrl,
    employmentType,
    jobDescription,
    location,
    rating,
    title,
  } = jobDetails

  return (
    <li className="similar-job-item">
      <div className="job-card">
        <div className="job-header">
          <img
            src={companyLogoUrl}
            alt="similar job company logo"
            className="company-logo"
          />
          <h1 className="job-title">{title}</h1>
        </div>
        <div className="job-rating">
          <img
            src="https://assets.ccbp.in/frontend/react-js/star-img.png"
            alt="star"
            className="star"
          />
          <p className="rating">{rating}</p>
        </div>
        <p>Description</p>
        <p className="job-description">{jobDescription}</p>
        <div className="job-card-info">
          <div className="job-location">
            <FaMapMarkerAlt className="info-icon" />
            <p className="info-text">{location}</p>
          </div>
          <div className="job-employment">
            <FaSuitcase className="info-icon" />
            <p className="info-text">{employmentType}</p>
          </div>
        </div>
      </div>
    </li>
  )
}

export default SimilarJobItem

                                                           #SimilarJobItem ./index.css

.similar-job-item {
  list-style-type: none;
  margin: 10px;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 8px;
  background-color: #1a1a1a;
  color: white;
  width: 300px;
}

.job-card {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.job-header {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 10px;
}

.company-logo {
  width: 40px;
  height: 40px;
}

.job-title {
  font-size: 18px;
  font-weight: bold;
}

.job-rating {
  display: flex;
  align-items: center;
  gap: 5px;
  margin-bottom: 10px;
}

.rating {
  font-size: 16px;
  color: #fbc02d;
}

.star {
  width: 16px;
  height: 16px;
}

.company-name {
  font-size: 16px;
  margin-bottom: 10px;
}

.job-description {
  font-size: 14px;
  margin-bottom: 10px;
  text-align: center;
}

.job-card-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap; /* Ensures proper alignment on smaller screens */
  margin-bottom: 16px;
}

.job-location,
.job-employment {
  display: flex;
  align-items: center;
  margin-right: 20px; 
}

.info-icon {
  color: #64748b; 
  margin-right: 8px;
}

.info-text {
  font-size: 16px;
  color: #cbd5e1; 
}

                                                                         #App.Css 
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}


                                                                             #App.js

import {
  Route,
  Switch,
  Redirect,
} from 'react-router-dom'
import LoginForm from './components/LoginForm'
import Home from './components/Home'
import Jobs from './components/Jobs'
import JobDetails from './components/JobDetails'
import NotFound from './components/NotFound'
import ProtectedRoute from './components/ProtectedRoute'

import './App.css'

const App = () => (
  <>
    <Switch>
      <Route exact path="/login" component={LoginForm} />
      <ProtectedRoute exact path="/" component={Home} />
      <ProtectedRoute exact path="/jobs" component={Jobs} />
      <ProtectedRoute exact path="/jobs/:id" component={JobDetails} />
      <Route path="/not-found" component={NotFound} />
      <Redirect to="not-found" />
    </Switch>
  </>
)

export default App



                                                                            #index.js

import React from 'react'
import ReactDOM from 'react-dom'
import {BrowserRouter} from 'react-router-dom'

import App from './App'

ReactDOM.render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>,
  document.getElementById('root'),
)

                                                                             
