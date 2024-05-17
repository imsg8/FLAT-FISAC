```mermaid
flowchart TB
    subgraph GRU
        Input[Inputs: h_{t-1}, x_t]

        ResetGate[Reset Gate]
        ResetGateCalc[Calculate r_t = \sigma(W_r * [h_{t-1}, x_t])]
        ResetGate --> ResetGateCalc

        UpdateGate[Update Gate]
        UpdateGateCalc[Calculate z_t = \sigma(W_z * [h_{t-1}, x_t])]
        UpdateGate --> UpdateGateCalc

        CandidateActivation[Candidate Activation]
        CandidateActivationCalc[Calculate \tilde{h}_t = tanh(W * [r_t * h_{t-1}, x_t])]
        CandidateActivation --> CandidateActivationCalc

        NewHiddenState[New Hidden State]
        NewHiddenStateCalc[Calculate h_t = (1 - z_t) * h_{t-1} + z_t * \tilde{h}_t]
        NewHiddenState --> NewHiddenStateCalc

        Input --> ResetGate
        Input --> UpdateGate
        ResetGateCalc --> CandidateActivation
        Input --> CandidateActivation
        CandidateActivationCalc --> NewHiddenState
        UpdateGateCalc --> NewHiddenState
    end

    Output[Output: h_t]
    GRU --> Output
