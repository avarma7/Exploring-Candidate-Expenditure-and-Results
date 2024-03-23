# Exploring-Candidate-Expenditure-and-Results
Additional Contributors: hindskre000, egmenton, pantraci

## Project Description
We used public disclosure data about campaign funding and expenditures of candidates running for office within Washington State counties to find patterns in campaign spending based on political party, office, and other variables. We visualized these findings and created an interactive dashboard to effectively display our visualizations. We would like to see if a candidate's expenditure toward an election corresponds to how well they do in the election. For this, we combined the expenditures dataset with a dataset containing the election results for all Washington counties since 2014. With this, we created predictive models to predict the percentage of votes a candidate received according to their expenditure and other categorical variables such as office and party.

## Table Description (Expenditure Dataset)
Link: https://data.wa.gov/Politics/Expenditures-by-Candidates-and-Political-Committee/tijg-9zyp/data

Dataset includes expenditures since 2014 as reported to the PDC
In-kind contributions (non-monetary) included as they are considered as both a contribution and expenditure.
How number of years are determined:
Candidates: determined by year of the election
Political Committees: determined by calendar year of the reporting period.
Candidates and political committees choosing to file under "mini reporting" not included in dataset.

## Table Column Descriptions
id : PDC internal identifier that correspond to a single expenditure record.

report_number : PDC identifier for tracking individual form C4. Expenditures that were reported to the PDC at the same time have the same report number. For amended report, only the most recent report number is included in the dataset.

origin : shows from which filed report-type the data originates.

A/LE50: non-itemized expenditures of $200 and less per expenditure.
A/GT50: itemized expenditures greater that $200 per expenditure.
Inflationary rule changes dollar amount on April 1, 2023 from $50 and less expenditure to $200 and less per expenditure.
committee_id : unique identifier of a committee.

*Continuing committee has the same id for all years registered. *Single year committees and candidate committees have an uniqie identifier each year. *Surplus accounts have single committee id all year.

filer_id : unique id assigned to candidate or political committee.

*Consistent across election years except for ones who run a second office in the same election year will receive two filer_id. *for a candidate and single-election year committee such as a ballot committee, the combination of filter_id and election year uniquely identifies a campaign

type : indicate if record is for candidate or political committee. Political committee may be either a continuing political committee, party committee, or single election year committee.

filer_name : candidate or committee name reported on form C1 candidate or committee registration form. Name may be differ accross years if candidates or committees change their name.

office : office sought by candidate. Doesn't apply to political committees.

legislative_district : Washington State legislative district. Only applies to condidates where office is "state senator" or "state representative."

position : Position associated with an office. This field typically applies to judicial and local office that have multiple positions or seats. Does not apply to political committees.

party : political party declared by the candidate or committee on their form C1 registration. Only contains "major parties" recognized by Washington State law.

ballot_number : Statewide Ballot Initiative committee has a ballot number assigned by the Secretary of State. Local Ballot Initiatives do not have a ballot number.

for_or_against : Ballot initiative committes are formed to support or oppose an initiative. This field represents if a committee "supports" or "opposes" a ballot initiative.

jurisdiction : Political jurisdiction associated with the office of a candidate.

jurisdiction_county : county associated with the jurisdiction of a candidate. Multi-county jurisdictions as reported as the primary county. This field will be empty for political commitees and when a candidate jurisdiction is statewide.

jurisdiction_type : type of jurisdiction this office is.

election_year : election year in the case of candidates and single election committees. For continuing political committees, it will be their reporting year.

amount : amount of the expenditure or in-kind contribution.

itemized_or_non_itemized : a record for itemized and non-itemized expenditure.

*Itemized: represents a single expenditure *Non-itemized: represent one or more expenditures where the individual expenditures are less than the limit for itemized reporting. In this case, the record is the aggregate total for the reporting period.

expenditure_date : date that the expenditure was made or the in-kind contribution was received.

description : reported description of the transaction. Non-itemized expenditures will not contain a description.

code : the type of expenditure. Refer to form C4 schedule for a listing of all codes. Itemized expenditures have a description or code.

recipient_address : street address of the individual or vendor paid as reported.

recipient_city : city of the individual or vendor paid as reported.

recipient_state : state of the individual or vendor paid as reported.

recipient_zip : zip code of the individual or vendor paid as reported.

url : a link to PDF version of the original report as it was filed to the PDC.

recipient_location : N/A (no description included)

payee : A campaign may reimburse a person or entity or expenses they occurred on behalf of the campaign. In those cases, subcontractor, business that provided the products, or services will appear as the recipient and the person or entity who was paid or reimbursed for procuring the services or products is the payee.

creditor : the person, vendor, or entity to whom the campaign debt is owned.

## Table Description (Election Results)
Link: https://www.sos.wa.gov/elections/data-research/election-data-and-maps/election-results-and-voters-pamphlets

The website has the results for each year for each county in a separate csv file. We combined all the election results csv files for years since 2014 for all counties into one file and proceeded from there to combine this with the expenditures data. 

## Table Column Descriptions
race : description of certain district

CountyCode : abbreviation of counties in WA state

Candidate : name of the condidate

PrecinctName: name of precinct or voting district

PrecinctCode : code that represents a precinct or voting district

Votes : number of votes recieved for candidate


## Modeling Results
In the data, we have a PercentageOfTotalVotes variable which served as our response variable. We implemented a Multiple Linear Regression and a Random Forest model to try to predict PercentageOfTotalVotes with a candidate's total expenditure and mean expenditure amount as the main predictors. 

After implementing both of these models, unfortunately, we did not get the results we were expecting. We found that there was little to no correlation between expenditure and the percentage of total votes a candidate received. For both models we had a RMSE value of about 17, which is quite high and implies poor model accuracy, likely due to the low correlation between the predictors and response. We also tried variable transformations on the predictors as well as target encoding on the office and party categorical variables, however, we were unable to lower the RMSE value for the models. So, from this data alone, we concluded that the amount a candidate spends for an election does not really correspond to how well they will do in an election, but we believe that we may be missing some crucial information or a predictor that is not present in our chosen datasets.

## Next Steps
We believe that we may be missing some important predictors in our data that could help better explain the relationship we were exploring. Also, the data had many categorical variables which is not optimal for modeling situations. Better exploratory analysis could have informed us that the data was not a right fit for what we plan to do much sooner. 
If we were to repeat, we would try to pick our datasets more carefully or try to find more meaningful predictors. We could also analyze correlation between votes and expendture in different election types, such as a presidential election. 
