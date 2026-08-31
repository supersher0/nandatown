# Pricing Strategy Experiment: Seller Price Multiplier

## Experiment Overview

**Scenario:** Marketplace (50 buyers, 50 sellers)  
**Setting Changed:** `seller_price_multiplier` from 1.0 (default) to 1.2 (20% markup)  
**Seeds:** Both used seed 42 for reproducibility

## Hypothesis

If sellers start their initial offers 20% higher than baseline, negotiations will take longer and deal completion rates will drop because buyers reject more high-priced offers. I expected to see:
- Lower deal_rate (fewer successful transactions)
- Higher rejection_rate (buyers saying no more often)
- Higher mean_rounds_to_deal (longer negotiations)

## Results

### Baseline (Original)


deal_rate: 0.5320
rejection_rate: 0.4680
mean_rounds_to_deal: 1.0226
message_count: 2000

With 20% Seller Markup
deal_rate:            0.5320
rejection_rate:       0.4680
mean_rounds_to_deal:  1.0226
message_count:        2000

Finding: No measurable difference. All metrics identical.

Investigation

The surprising result prompted investigation:

Verified the setting was applied: Confirmed seller_price_multiplier: 1.2 was in the YAML file before running
Checked both traces ran: Both completed without errors, wrote 2000 messages each
Ran validators: Both scenarios passed all marketplace protocol validators
Compared agent behavior: Top sellers in both runs sent identical numbers of messages (seller-15: 15 sends, seller-18: 15 sends, etc.)

Possible explanations:

The parameter may not be connected to the negotiation layer's pricing logic
The alternating_offers negotiation strategy might use relative pricing adjustments rather than absolute prices
Both runs used the same seed (42), so agent behavior patterns may be deterministic regardless of initial pricing
The seller_price_multiplier parameter name might not match the actual configuration key the code expects
Conclusion

The experiment successfully ran but revealed that the seller_price_multiplier setting, as currently implemented, does not affect marketplace outcomes. This could indicate either a parameter naming/implementation mismatch or that the negotiation strategy is robust to initial pricing variations through its bargaining mechanism.

Tools & Help Used
NANDA Town CLI (nest run, nest inspect, nest report, nest validators)
Nano text editor for YAML editing
Claude for hypothesis design and investigation guidance
GitHub markdown for documentation
# Pricing Strategy Experiment: Seller Price Multiplier

## Experiment Overview
Scenario: Marketplace with 100 agents
Setting Changed: seller_price_multiplier from 1.0 to 1.2 (20% higher)

## Hypothesis
If sellers start 20% higher, deal rates will drop and rejections increase because buyers reject expensive offers.

## Results

**Baseline:**
- deal_rate: 0.5320
- rejection_rate: 0.4680
- mean_rounds_to_deal: 1.0226
- message_count: 2000

**With 20% Markup:**
- deal_rate: 0.5320
- rejection_rate: 0.4680
- mean_rounds_to_deal: 1.0226
- message_count: 2000

**Finding:** No change. All metrics identical.

## Investigation

Surprisingly, the 20% price markup had zero effect on outcomes. I verified:
1. The setting was correctly added to the YAML file
2. Both scenarios ran without errors
3. Both passed all validators
4. Agent behavior was identical

**Why?** Possible reasons:
- The seller_price_multiplier parameter may not be wired to the negotiation logic
- The alternating_offers strategy uses relative pricing, not absolute prices
- Same seed (42) means identical agent paths regardless of pricing
- Parameter name may not match the actual implementation

## Tools Used
- NANDA Town CLI
- Nano text editor
- Claude for guidance

