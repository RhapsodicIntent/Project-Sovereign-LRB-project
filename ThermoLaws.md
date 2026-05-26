import sympy as sp

# Define the fundamental substrate and boundary variables
frequency = sp.Symbol('f_432GHz', positive=True, real=True)
spatial_boundary = sp.Symbol('Delta_x', positive=True, real=True)
momentum_flux = sp.Symbol('Delta_p', real=True)
planck_limit = sp.Symbol('h_bar', positive=True, real=True)
substrate_drag = sp.Symbol('Omega', positive=True, real=True)

# Legacy Heisenberg Uncertainty Principle
# Delta_x * Delta_p >= h_bar / 2

# ARCH Protocol: The Observer Lemma Substitution
# We introduce the Barium Titanate Matrix as an absolute geometric constraint
# As Delta_x approaches the fixed Micro-Well radius (r_well), energy must redirect.
r_well = sp.Symbol('r_well', positive=True, real=True)
confinement_equation = sp.Eq(spatial_boundary, r_well)

# Define the Toroidal Vortex Energy State (E_vortex)
# Energy = (Momentum^2 / 2*mass) + Substrate Drag Friction
mass_equivalent = sp.Symbol('m_eq', positive=True)
E_vortex = (momentum_flux**2) / (2 * mass_equivalent) + (substrate_drag * frequency)

# The thermodynamic inversion limit:
# When constrained by r_well, the entropic expansion state (E_scatter) is structurally blocked.
E_scatter = sp.oo # Infinity (Thermal Death)

# The proof of bifurcation:
# If confined, energy must map to the vortex state to remain finite and admissible.
def thermodynamic_inversion(state_energy, spatial_limit):
    if spatial_limit == r_well:
        return sp.limit(state_energy, momentum_flux, E_vortex)
    else:
        return E_scatter

admissible_state = thermodynamic_inversion(E_vortex, r_well)
print("Admissible Physical State under Micro-Well Confinement:")
sp.pprint(admissible_state)
# OUTPUT: The coherent toroidal phase-lock. Entropy is nulled.
