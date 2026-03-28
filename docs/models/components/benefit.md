# Benefit


## Supported Types

### BenefitCustom

```go
benefit := components.CreateBenefitBenefitCustom(components.BenefitCustom{/* values here */})
```

### BenefitDiscord

```go
benefit := components.CreateBenefitBenefitDiscord(components.BenefitDiscord{/* values here */})
```

### BenefitGitHubRepository

```go
benefit := components.CreateBenefitBenefitGitHubRepository(components.BenefitGitHubRepository{/* values here */})
```

### BenefitDownloadables

```go
benefit := components.CreateBenefitBenefitDownloadables(components.BenefitDownloadables{/* values here */})
```

### BenefitLicenseKeys

```go
benefit := components.CreateBenefitBenefitLicenseKeys(components.BenefitLicenseKeys{/* values here */})
```

### BenefitMeterCredit

```go
benefit := components.CreateBenefitBenefitMeterCredit(components.BenefitMeterCredit{/* values here */})
```

## Union Discrimination

Use the `Type` field to determine which variant is active, then access the corresponding field:

```go
switch benefit.Type {
	case components.BenefitUnionTypeBenefitCustom:
		// benefit.BenefitCustom is populated
	case components.BenefitUnionTypeBenefitDiscord:
		// benefit.BenefitDiscord is populated
	case components.BenefitUnionTypeBenefitGitHubRepository:
		// benefit.BenefitGitHubRepository is populated
	case components.BenefitUnionTypeBenefitDownloadables:
		// benefit.BenefitDownloadables is populated
	case components.BenefitUnionTypeBenefitLicenseKeys:
		// benefit.BenefitLicenseKeys is populated
	case components.BenefitUnionTypeBenefitMeterCredit:
		// benefit.BenefitMeterCredit is populated
}
```
