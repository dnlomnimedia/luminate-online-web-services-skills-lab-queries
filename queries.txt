# Basic info for all constituents
SELECT ConsId, ConsName.FirstName, ConsName.LastName, PrimaryEmail From Constituent

# Basic info for a constituent with email address 'joe.landsman@gmail.com'
SELECT ConsId, ConsName.FirstName, ConsName.LastName, PrimaryEmail From Constituent WHERE PrimaryEmail = 'joe.landsman@gmail.com'

# Basic info for all constituents in a Group 49504
SELECT ConsId, ConsName.FirstName, ConsName.LastName, PrimaryEmail From Constituent WHERE GroupId = 49504

# Basic info for all constituents updated after 2021-11-09T00:00:00 UTC
SELECT ConsId, ConsName.FirstName, ConsName.LastName, PrimaryEmail From Constituent WHERE ModifyDate > 2021-11-09T00:00:00Z

# All Donations
SELECT TransactionId, FormId, Payment.Amount, Payment.PaymentDate, Donor.ConsId From Donation

# Donations to form 2726
SELECT TransactionId, FormId, Payment.Amount, Payment.PaymentDate, Donor.ConsId From Donation WHERE FormId = 2726

# Donations made after 2021-11-09T00:00:00 UTC
SELECT TransactionId, FormId, Payment.Amount, Payment.PaymentDate, Donor.ConsId From Donation WHERE Payment.PaymentDate > 2021-11-09T00:00:00Z

# Donations that are from an active recurring series
SELECT TransactionId, FormId, Payment.Amount, Payment.PaymentDate, Donor.ConsId, RecurringPayment.Type, RecurringPayment.Status From Donation WHERE RecurringPayment.Status = 'ACTIVE'

# Donations that were the first in a recurring series
SELECT TransactionId, FormId, Payment.Amount, Payment.PaymentDate, Donor.ConsId, RecurringPayment.OriginalTransactionId From Donation WHERE TransactionId = RecurringPayment.OriginalTransactionId

# Donations greater than $1000 this year
SELECT TransactionId, FormId, Payment.Amount, Payment.PaymentDate, Donor.ConsId From Donation WHERE Payment.PaymentDate > 2021-01-01 AND Payment.Amount > 1000

# Active Recurring Gifts
SELECT RecurringAmount, Frequency, Duration, Status FROM RecurringPayment WHERE Status = 'ACTIVE'

# Recurring Gifts cancelled by Donor
SELECT RecurringAmount, Frequency, Duration, Status FROM RecurringPayment WHERE Status = 'USER_CANCELLED'

# Survey Responses to Survey 2801 (does not include user registration or 'unlimited text' field data)
SELECT ConsId, Answer FROM SurveyResponse WHERE SurveyId = 2801

# Teamraiser Events
SELECT EventId, Title, Name, Status, EventDate, Goal FROM TeamRaiserEvent

# Teamraiser Events currently accepting registrations
SELECT EventId, Title, Name, Status, EventDate, Goal FROM TeamRaiserEvent WHERE Status = 'ACCEPT_REGISTRATION'

# Teamraiser Teams for Event 1300
SELECT TeamId, Name, Description, Goal, IsPrivate FROM TeamRaiserTeam WHERE EventId = 1300

# Teamraiser Gifts for Event 1300
SELECT GiftId, EventId, TeamId, Type, TransactionId, GiftAmount FROM TeamRaiserGift WHERE EventId = 1300

# Teamraiser Gifts for Team 1390 in Event 1300
SELECT GiftId, EventId, TeamId, Type, TransactionId, GiftAmount FROM TeamRaiserGift WHERE EventId = 1300 AND TeamId = 1390
